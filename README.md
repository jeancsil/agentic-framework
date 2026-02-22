# Agentic Framework

A LangChain + MCP framework for building agentic systems in Python 3.12+.

![Build Status](https://github.com/jeancsil/agentic-framework/actions/workflows/ci.yml/badge.svg)
![Python Version](https://img.shields.io/badge/python-3.12%2B-blue)
![GitHub License](https://img.shields.io/github/license/jeancsil/agentic-framework)

## What is this?

This framework helps you build AI agents that can:
- Use **local tools** (file operations, code search, etc.)
- Connect to **MCP servers** (web search, flight booking, etc.)
- Combine both in a single runtime

**Key features:**
- Decorator-based agent registration with automatic CLI generation
- Reusable LangGraph agent pattern with checkpointing
- Per-agent MCP server permissions
- Multi-language code navigation tools
- Safe file editing with automatic syntax validation

## Quick Start

```bash
# Install dependencies
make install

# Run tests
make test

# List available agents
uv --directory agentic-framework run agentic-run list

# Run the developer agent
uv --directory agentic-framework run agentic-run developer -i "Explain the project structure"
```

## Available Agents

| Agent | Purpose | MCP Access | Tools |
|-------|---------|------------|-------|
| `developer` | Codebase exploration & editing | webfetch | find_files, discover_structure, get_file_outline, read_file_fragment, code_search, edit_file |
| `travel-coordinator` | Multi-agent trip planning | kiwi-com-flight-search, web-fetch | Orchestrates 3 specialist agents |
| `chef` | Recipe suggestions | tavily | web_search |
| `news` | AI news aggregation | web-fetch | - |
| `travel` | Flight search | kiwi-com-flight-search | - |
| `simple` | Basic conversation | none | - |

## CLI Reference

```bash
# List all agents
uv --directory agentic-framework run agentic-run list

# Get agent info
uv --directory agentic-framework run agentic-run info <agent>

# Run an agent
uv --directory agentic-framework run agentic-run <agent> -i "your input"

# With timeout (seconds)
uv --directory agentic-framework run agentic-run <agent> -i "input" -t 120

# Verbose logging
uv --directory agentic-framework run agentic-run <agent> -i "input" -v
```

## Developer Agent

The `developer` agent is a Principal Software Engineer assistant for codebase work.

**Available tools:**

| Tool | Description | Input Format |
|------|-------------|--------------|
| `find_files` | Search files by name | `pattern` |
| `discover_structure` | Directory tree | `[max_depth]` |
| `get_file_outline` | Extract signatures | `file_path` |
| `read_file_fragment` | Read line range | `path:start:end` |
| `code_search` | Pattern search | `pattern` |
| `edit_file` | Edit files | See below |

**Supported languages for `get_file_outline`:** Python, JavaScript, TypeScript, Rust, Go, Java, C/C++, PHP

**File editing workflow:**
```bash
# Search/replace (recommended - no line numbers needed)
{"op": "search_replace", "path": "file.py", "old": "exact text", "new": "new text"}

# Line-based operations
replace:path:start:end:content
insert:path:after_line:content
delete:path:start:end
```

## Multi-Agent Systems

The `travel-coordinator` demonstrates multi-agent orchestration:

```bash
uv --directory agentic-framework run agentic-run travel-coordinator -i "Plan a 5-day trip from Lisbon to Berlin in May"
```

**Workflow:**
1. `FlightSpecialistAgent` → gathers flight options
2. `CityIntelAgent` → adds destination intelligence
3. `TravelReviewerAgent` → final itinerary

## Docker Support

```bash
# Build image
make docker-build

# Run agents
bin/agent.sh developer -i "Search for all Tool definitions"
bin/agent.sh chef -i "I have bread, tuna, lettuce and mayo"

# View logs
tail -f agentic-framework/logs/agent.log
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_MODEL_NAME` | No | LLM model (default: gpt-4) |
| `OPENAI_API_KEY` | Yes | OpenAI API key |
| `TAVILY_API_KEY` | For chef agent | Tavily search API |
| `TINYFISH_API_KEY` | Optional | TinyFish MCP access |

## Building New Agents

### Minimal Agent

```python
from agentic_framework.core.langgraph_agent import LangGraphMCPAgent
from agentic_framework.registry import AgentRegistry

@AgentRegistry.register("my-agent", mcp_servers=["tavily"])
class MyAgent(LangGraphMCPAgent):
    @property
    def system_prompt(self) -> str:
        return "You are my custom agent."
```

### Agent with Local Tools

```python
from langchain_core.tools import StructuredTool
from agentic_framework.core.langgraph_agent import LangGraphMCPAgent
from agentic_framework.registry import AgentRegistry

@AgentRegistry.register("my-agent", mcp_servers=None)
class MyAgent(LangGraphMCPAgent):
    @property
    def system_prompt(self) -> str:
        return "You are a helpful assistant."

    def local_tools(self) -> list:
        return [
            StructuredTool.from_function(
                func=my_function,
                name="my_tool",
                description="What this tool does",
            )
        ]
```

### Multi-Agent Coordinator

```python
from agentic_framework.interfaces.base import Agent
from agentic_framework.registry import AgentRegistry

@AgentRegistry.register("coordinator", mcp_servers=["server1", "server2"])
class CoordinatorAgent(Agent):
    async def run(self, input_data, config=None):
        # Stage 1: First specialist
        specialist1 = Specialist1Agent()
        result1 = await specialist1.run(input_data)

        # Stage 2: Second specialist
        specialist2 = Specialist2Agent()
        result2 = await specialist2.run(result1)

        return result2

    def get_tools(self):
        return []
```

After creating your agent in `src/agentic_framework/core/`, it automatically becomes available:

```bash
uv --directory agentic-framework run agentic-run my-agent -i "hello"
```

## Architecture

```
User Input
    │
    ▼
┌─────────────────┐
│   CLI (Typer)   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     ┌─────────────────┐
│ AgentRegistry   │────▶│ Agent Discovery │
└────────┬────────┘     └─────────────────┘
         │
         ▼
┌─────────────────┐     ┌─────────────────┐
│  MCPProvider    │────▶│  MCP Servers    │
└────────┬────────┘     └─────────────────┘
         │
         ▼
┌─────────────────┐
│ LangGraph Agent │
│  (base class)   │
└────────┬────────┘
         │
    ┌────┴────┐
    ▼         ▼
┌───────┐ ┌───────┐
│ Local │ │  MCP  │
│ Tools │ │ Tools │
└───────┘ └───────┘
```

**Key files:**
- `src/agentic_framework/core/langgraph_agent.py` - Reusable agent base
- `src/agentic_framework/registry.py` - Agent registration
- `src/agentic_framework/mcp/provider.py` - MCP connection management
- `src/agentic_framework/tools/` - Tool implementations

## Development

```bash
make install    # Install dependencies
make test       # Run tests (coverage threshold: 60%)
make lint       # Run mypy + ruff
make format     # Auto-format code
make check      # Run all checks (lint + format check)
```

**Before committing:** Run `make check && make test`

## License

MIT License - see [LICENSE](LICENSE) for details.
