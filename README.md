<div align="center">

<<<<<<< ours
A LangChain + MCP framework for building agentic systems in Python 3.12+.
||||||| ancestor
An educational LangChain + MCP framework for learning and building agentic systems in Python 3.12+.
=======
# 🤖 Agentic Framework
**Build AI agents that *actually* do things.**
>>>>>>> theirs

[![Python 3.12+](https://img.shields.io/badge/python-3.12%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangChain](https://img.shields.io/badge/langchain-%23007BA7.svg?style=for-the-badge&logo=langchain&logoColor=white)](https://python.langchain.com/)
[![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-green?style=for-the-badge)](https://modelcontextprotocol.io/)
[![Docker Ready](https://img.shields.io/badge/docker-ready-blue?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![License](https://img.shields.io/github/license/jeancsil/agentic-framework?style=for-the-badge)](LICENSE)
[![CI](https://img.shields.io/github/actions/workflow/status/jeancsil/agentic-framework/ci.yml?style=for-the-badge&logo=github&label=Build)](https://github.com/jeancsil/agentic-framework/actions)
[![Coverage](https://img.shields.io/badge/coverage-80%25-brightgreen?style=for-the-badge)](https://github.com/jeancsil/agentic-framework)

<<<<<<< ours
## What is this?
||||||| ancestor
## Goal of This Repository
=======
<br>
>>>>>>> theirs

<<<<<<< ours
This framework helps you build AI agents that can:
- Use **local tools** (file operations, code search, etc.)
- Connect to **MCP servers** (web search, flight booking, etc.)
- Combine both in a single runtime
||||||| ancestor
This project is intentionally small so you can learn the core building blocks of agentic coding:
=======
Combine **local tools** and **MCP servers** in a single, elegant runtime.  
Write agents in **5 lines of code**. Run them anywhere.
>>>>>>> theirs

<<<<<<< ours
**Key features:**
- Decorator-based agent registration with automatic CLI generation
- Reusable LangGraph agent pattern with checkpointing
- Per-agent MCP server permissions
- Multi-language code navigation tools
- Safe file editing with automatic syntax validation
||||||| ancestor
- agent registry and dynamic CLI commands
- reusable LangGraph agent pattern
- optional MCP server access with explicit per-agent permissions
- local tools + MCP tools combined in one runtime
- testable architecture (no network required in unit tests)
=======
[Quick Start](#-quick-start-zero-to-agent-in-60s) • [Build an Agent](#-build-your-own-agent) • [Architecture](#-architecture) • [Demo](#-see-it-in-action)
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
## Prerequisites
=======
</div>
>>>>>>> theirs

<<<<<<< ours
## Quick Start (Docker - Recommended)
||||||| ancestor
- Python >= 3.12, < 3.14
- [uv](https://docs.astral.sh/uv/) (recommended)
=======
---
>>>>>>> theirs

<<<<<<< ours
**Docker is the recommended way to run this framework.** It comes pre-configured with all required tools and dependencies.
||||||| ancestor
## Quickstart
=======
## 🎬 See it in Action
>>>>>>> theirs

<<<<<<< ours
```bash
# Build the Docker image
make docker-build
||||||| ancestor
```bash
make install
make test
```
=======
<p align="center">
  <a href="https://asciinema.org/a/YOUR_CAST_ID_HERE" target="_blank">
    <img src="https://asciinema.org/a/YOUR_CAST_ID_HERE.svg" alt="Agentic Framework Demo" width="100%">
  </a>
</p>

> 💡 *Pro-tip: Record your own demo with `asciinema rec` and replace the embed above!*
>>>>>>> theirs

# Run agents (no rebuild needed for code changes)
bin/agent.sh developer -i "Explain project structure"
bin/agent.sh chef -i "I have eggs and cheese"
bin/agent.sh list

<<<<<<< ours
# View logs (same location as local)
tail -f agentic-framework/logs/agent.log
||||||| ancestor
```bash
uv --project agentic-framework run agentic-run developer -i "List the project structure and explain what the main components do."
=======
## ✨ Why Agentic Framework?

| ⚡ Rapid Prototyping | 🐋 Production Isolation | 🔌 Protocol Native |
|---|---|---|
| **Zero-Config Registry.** Register agents with a single decorator. Auto-discovers in CLI. | **Docker-First.** Every agent is isolated. No "it works on my machine" excuses. | **MCP Ready.** Native support for the Model Context Protocol ecosystem. |

| 🧬 Stateful Runtimes | 🧩 Multi-Agent Mesh | ⚡ Codebase Context |
|---|---|---|
| **LangGraph Core.** Supports checkpointing, cycles, and human-in-the-loop. | **Orchestration.** Chain specialized agents like Lego blocks for complex tasks. | **Local Power Tools.** Integrated `ripgrep`, `fd`, and AST parsing for real context. |

# Access logs (same location as local)
tail -f agentic-framework/logs/agent.log
>>>>>>> theirs
```

<<<<<<< ours
**Why Docker?**
- All dependencies pre-installed: `ripgrep`, `fd`, `fzf`, `tree-sitter`
- No environment setup needed - just build and run
- Code changes reflected immediately (mounted volumes)
- Consistent environment across all machines

---

## Local Installation

If you need to run locally, you must install these dependencies:

**System packages:**
- `ripgrep` - Ultra-fast text searching
- `fd` - User-friendly alternative to `find`
- `fzf` - General-purpose command-line fuzzy finder

**Python packages (managed by `uv`):**
- `tree-sitter` - Parser generator
- `tree-sitter-languages` - Grammar packages
||||||| ancestor
List all available agents:
=======
## 🚀 Quick Start (Zero to Agent in 60s)

### 1️⃣ Add your Brain (API Key)
You need an **LLM API key** to breathe life into your agents.
>>>>>>> theirs

```bash
<<<<<<< ours
# Install Python dependencies
make install

# Run tests
make test

# Run agents
uv --directory agentic-framework run agentic-run developer -i "Explain project structure"
```
||||||| ancestor
uv --project agentic-framework run agentic-run list
```
=======
# Copy the template
cp .env.example .env
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
## Docker Support 🐳
=======
# Edit .env and paste your OpenAI key
# OPENAI_API_KEY=sk-your-key-here
```
> ⚠️ **Note:** At minimum, set `OPENAI_API_KEY`. Without it, your agents will sleep forever! 💤
>>>>>>> theirs

<<<<<<< ours
## Available Tools
||||||| ancestor
Run the framework in Docker with mounted volumes for live code updates:
=======
### 2️⃣ Build & Run
No `pip`, no `virtualenv`, no *"it works on my machine"* excuses.
>>>>>>> theirs

<<<<<<< ours
| Tool | Purpose | Input Format |
|-------|---------|--------------|
| `find_files` | Fast file search via `fd` | `pattern` |
| `discover_structure` | Directory tree exploration | `[max_depth]` (default: 3) |
| `get_file_outline` | Extract class/function signatures | `file_path` |
| `read_file_fragment` | Read specific line ranges | `path:start:end` (1-indexed) |
| `code_search` | Pattern search via `ripgrep` | `regex_pattern` |
| `edit_file` | Safe file editing with syntax validation | See below |
| `web_search` | Web search via Tavily | `query` |
||||||| ancestor
```bash
# Build the Docker image
make docker-build
=======
```bash
# Clone the repository
git clone https://github.com/jeancsil/agentic-framework.git
cd agentic-framework

# Build the Docker image
make docker-build
>>>>>>> theirs

<<<<<<< ours
### File Editing
||||||| ancestor
# Run agents using the shell wrapper
bin/agent.sh developer -i "Search for all Tool definitions in the project"
bin/agent.sh chef -i "I have bread, tuna, lettuce and mayo"
bin/agent.sh list
=======
# Unleash your first agent!
bin/agent.sh developer -i "Explain this codebase"
>>>>>>> theirs

<<<<<<< ours
**RECOMMENDED: search_replace (no line numbers needed)**
```json
{"op": "search_replace", "path": "file.py", "old": "exact text", "new": "replacement text"}
||||||| ancestor
# Access logs (same location as local)
tail -f agentic-framework/logs/agent.log
=======
# Or try the chef agent
bin/agent.sh chef -i "I have chicken, rice, and soy sauce. What can I make?"
>>>>>>> theirs
```

<<<<<<< ours
**Line-based operations:**
```
replace:path:start:end:content
insert:path:after_line:content
delete:path:start:end
```
||||||| ancestor
**Key Features:**
- ✅ No rebuild needed when changing Python code (mounted volumes)
- ✅ Environment variables safely loaded from `.env`
- ✅ Logs accessible from host machine
- ✅ Uses `uv` just like local development
- ✅ Simple shell wrapper mimics local CLI experience
=======
<details>
<summary><strong>🔑 Required Environment Variables</strong></summary>
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
=======
| Variable | Required? | Description |
|----------|-----------|-------------|
| `OPENAI_API_KEY` | 🟢 **Yes** | OpenAI API key (required for all agents) |
| `OPENAI_MODEL_NAME` | ⚪ No | Model to use (default: `gpt-4o`/`gpt-4`) |
>>>>>>> theirs

<<<<<<< ours
## Available MCP Servers
||||||| ancestor
## Featured Agents
=======
</details>
>>>>>>> theirs

<<<<<<< ours
| Server | Purpose | API Key Required |
|--------|---------|------------------|
| `kiwi-com-flight-search` | Flight search | No |
| `webfetch` | Web content fetching | No |
| `tavily` | Web search | Yes (`TAVILY_API_KEY`) |
| `tinyfish` | AI assistant | Yes (`TINYFISH_API_KEY`) |
||||||| ancestor
| Agent | What it does | MCP Access |
|---|---|---|
| `developer` | 🚀 **Principal Engineer** assistant for codebase exploration and search | `web-fetch` |
| `travel-coordinator` | ✈️ **Multi-agent Orchestrator** (Flights + City Intel + Reviewer) | `kiwi-com-flight-search`, `web-fetch` |
| `chef` | 🍳 Recipe suggestions from ingredients | `tavily` |
| `news` | 📰 AI news assistant (TechCrunch specialist) | `web-fetch` |
| `travel` | 🎫 Flight planning assistant | `kiwi-com-flight-search` |
| `simple` | 💬 Basic conversational chain | none |
=======
---
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
## Showcase: Developer Agent
=======
## 🏗️ Architecture
>>>>>>> theirs

<<<<<<< ours
## Available Agents
||||||| ancestor
The `developer` agent is designed to assist with codebase maintenance and understanding. It comes equipped with local tools for:
- **File Discovery**: Finding files by name across the project.
- **Structure Exploration**: Visualizing the project directory tree.
- **Code Outlining**: Extracting functions, classes, and signatures from code files.
  - Supports: Python, JavaScript, TypeScript, Rust, Go, Java, C/C++, PHP
  - Returns line numbers for precise navigation.
- **Pattern Search**: Global search using `ripgrep` for fast pattern matching.
=======
Under the hood, we seamlessly bridge the gap between user intent and execution:
>>>>>>> theirs

<<<<<<< ours
| Agent | Purpose | MCP Access | Tools |
|-------|---------|------------|-------|
| `developer` | Codebase exploration & editing | webfetch | find_files, discover_structure, get_file_outline, read_file_fragment, code_search, edit_file |
| `travel-coordinator` | Multi-agent trip planning | kiwi-com-flight-search, web-fetch | Orchestrates 3 specialist agents |
| `chef` | Recipe suggestions | tavily | web_search |
| `news` | AI news aggregation | web-fetch | - |
| `travel` | Flight search | kiwi-com-flight-search | - |
| `simple` | Basic conversation | none | - |
||||||| ancestor
Implementation: `src/agentic_framework/core/developer_agent.py`
=======
```mermaid
flowchart TB
    subgraph User [👤 User Space]
        Input[User Input]
    end
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
## Showcase: Travel Coordinator (Multi-Agent System)
=======
    subgraph CLI [💻 CLI - agentic-run]
        Typer[Typer Interface]
    end
>>>>>>> theirs

<<<<<<< ours
## CLI Reference
||||||| ancestor
Run:
=======
    subgraph Registry [📋 Registry]
        AR[AgentRegistry]
        AD[Auto-discovery]
    end
>>>>>>> theirs

<<<<<<< ours
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
||||||| ancestor
```bash
uv --project agentic-framework run agentic-run travel-coordinator -i "Plan a 5-day trip from Lisbon to Berlin in May."
```
=======
    subgraph Agents [🤖 Agents]
        Chef[chef agent]
        Dev[developer agent]
        Travel[travel agent]
    end

    subgraph Core [🧠 Core Engine]
        LGA[LangGraphMCPAgent]
        LG[LangGraph Runtime]
        CP[(Checkpointing)]
    end
>>>>>>> theirs

<<<<<<< ours
**In Docker:**
```bash
bin/agent.sh <agent> -i "input"
bin/agent.sh list
```

---

## Developer Agent

The `developer` agent is a Principal Software Engineer assistant for codebase work.

**Supported languages for `get_file_outline`:** Python, JavaScript, TypeScript, Rust, Go, Java, C/C++, PHP

---
||||||| ancestor
This example demonstrates complex orchestration using two remote MCP servers: `kiwi-com-flight-search` and `web-fetch`.
=======
    subgraph Tools [🧰 Tools & Skills]
        LT[Local Tools]
        MCP[MCP Tools]
    end

    subgraph External [🌍 External World]
        LLM[LLM API]
        MCPS[MCP Servers]
    end

    Input --> Typer
    Typer --> AR
    AR --> AD
    AR -->|Routes to| Chef & Dev & Travel

    Chef & Dev & Travel -->|Inherits from| LGA

    LGA --> LG
    LG <--> CP
    LGA -->|Uses| LT
    LGA -->|Uses| MCP

    LT -->|Reasoning| LLM
    MCP -->|Queries| MCPS
    MCPS -->|Provides Data| LLM

    LLM --> Output[Final Response]
```
>>>>>>> theirs

## Multi-Agent Systems

<<<<<<< ours
The `travel-coordinator` demonstrates multi-agent orchestration:
||||||| ancestor
1. **FlightSpecialistAgent** uses MCP tools to gather flight options.
2. **CityIntelAgent** receives the flight report and adds destination intelligence.
3. **TravelReviewerAgent** receives both reports and returns the final itinerary brief.
=======
## 🧰 Built-in Agents & Tools
>>>>>>> theirs

<<<<<<< ours
```bash
bin/agent.sh travel-coordinator -i "Plan a 5-day trip from Lisbon to Berlin in May"
```
||||||| ancestor
The coordinator implementation lives in: `src/agentic_framework/core/travel_coordinator_agent.py`
=======
### 🤖 Agents
>>>>>>> theirs

<<<<<<< ours
**Workflow:**
1. `FlightSpecialistAgent` → gathers flight options
2. `CityIntelAgent` → adds destination intelligence
3. `TravelReviewerAgent` → final itinerary
||||||| ancestor
## Architecture (Beginner-Friendly)
=======
| Agent | Purpose | MCP Servers | Local Tools |
|-------|---------|-------------|-------------|
| `developer` | **Codebase Master:** Explores, reads, and edits code safely. | `webfetch` | `find_files`, `discover_structure`, `get_file_outline`, `read_file_fragment`, `code_search`, `edit_file` |
| `travel-coordinator` | **Trip Planner:** Orchestrates multiple agents for seamless travel planning. | `kiwi-com-flight-search`, `webfetch` | *Orchestrates 3 sub-agents* |
| `chef` | **Culinary Genius:** Creates recipes based on what's in your fridge. | *web search via MCP* | `web_search` |
| `news` | **News Anchor:** Aggregates top stories. | `webfetch` | - |
| `travel` | **Flight Booker:** Finds the best routes. | `kiwi-com-flight-search` | - |
| `simple` | **Chat Buddy:** Basic conversational agent. | - | - |
>>>>>>> theirs

<<<<<<< ours
---
||||||| ancestor
Core flow:
=======
### 📦 Local Tools (Zero External Dependencies)
>>>>>>> theirs

<<<<<<< ours
## Environment Variables
||||||| ancestor
1. Register an agent in `src/agentic_framework/registry.py`.
2. CLI discovers registered agents and creates commands automatically.
3. If an agent has MCP permissions, CLI opens those MCP tool sessions.
4. Agent runs with local tools + MCP tools and returns final response.
=======
| Tool | Capability | Example |
|------|------------|---------|
| `find_files` | Lightning-fast search via `fd` | `*.py` finds all Python files |
| `discover_structure` | Directory tree mapping | Understands project layout |
| `get_file_outline` | AST-based signature parsing | Extracts classes and functions |
| `read_file_fragment` | Precise file reading | `file.py:10:50` |
| `code_search` | Hyper-fast text search via `ripgrep`| Global regex search |
| `edit_file` | Safe file editing | Inserts/Replaces lines |
>>>>>>> theirs

<<<<<<< ours
| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_MODEL_NAME` | No | LLM model (default: gpt-4) |
| `OPENAI_API_KEY` | Yes | OpenAI API key |
| `TAVILY_API_KEY` | For chef agent | Tavily search API |
| `TINYFISH_API_KEY` | Optional | TinyFish MCP access |
||||||| ancestor
Key files:
=======
### 🌐 MCP Servers (Context Superpowers)

| Server | Purpose | API Key Needed? |
|--------|---------|-----------------|
| `kiwi-com-flight-search` | Search real-time flights | 🟢 No |
| `webfetch` | Extract clean text from any URL | 🟢 No |
>>>>>>> theirs

---

<<<<<<< ours
## Building New Agents
||||||| ancestor
## Create a New Agent
=======
## 🛠️ Build Your Own Agent
>>>>>>> theirs

<<<<<<< ours
### Minimal Agent
||||||| ancestor
Minimal pattern:
=======
### The 5-Line Superhero 🦸‍♂️
>>>>>>> theirs

```python
from agentic_framework.core.langgraph_agent import LangGraphMCPAgent
from agentic_framework.registry import AgentRegistry

<<<<<<< ours
@AgentRegistry.register("my-agent", mcp_servers=["tavily"])
||||||| ancestor

@AgentRegistry.register("my-agent", mcp_servers=["tavily", "web-fetch"])
=======
@AgentRegistry.register("my-agent", mcp_servers=["webfetch"])
>>>>>>> theirs
class MyAgent(LangGraphMCPAgent):
    @property
    def system_prompt(self) -> str:
        return "You are my custom agent with the power to fetch websites."
```

Boom. Run it instantly:
```bash
bin/agent.sh my-agent -i "Summarize https://example.com"
```

<<<<<<< ours
### Agent with Local Tools
||||||| ancestor
Optional local tools:
=======
### Advanced: Custom Local Tools 🔧

Want to add your own Python logic? Easy.
>>>>>>> theirs

```python
<<<<<<< ours
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
||||||| ancestor
def local_tools(self):
    return [my_langchain_tool]
=======
from langchain_core.tools import StructuredTool
from agentic_framework.core.langgraph_agent import LangGraphMCPAgent
from agentic_framework.registry import AgentRegistry

@AgentRegistry.register("data-processor")
class DataProcessorAgent(LangGraphMCPAgent):
    @property
    def system_prompt(self) -> str:
        return "You process data files like a boss."

    def local_tools(self) -> list:
        return [
            StructuredTool.from_function(
                func=self.process_csv,
                name="process_csv",
                description="Process a CSV file path",
            )
        ]

    def process_csv(self, filepath: str) -> str:
        # Magic happens here ✨
        return f"Successfully processed {filepath}!"
>>>>>>> theirs
```

<<<<<<< ours
### Multi-Agent Coordinator
||||||| ancestor
## Build Complex Coordinators (No Base Changes)
=======
---

## 💻 CLI Reference
>>>>>>> theirs

<<<<<<< ours
```python
from agentic_framework.interfaces.base import Agent
from agentic_framework.registry import AgentRegistry
||||||| ancestor
Use this repeatable pattern for multi-agent systems:
=======
Command your agents directly from the terminal.
>>>>>>> theirs

<<<<<<< ours
@AgentRegistry.register("coordinator", mcp_servers=["server1", "server2"])
class CoordinatorAgent(Agent):
    async def run(self, input_data, config=None):
        # Stage 1: First specialist
        specialist1 = Specialist1Agent()
        result1 = await specialist1.run(input_data)
||||||| ancestor
1. Create small specialist classes that subclass `LangGraphMCPAgent`.
2. Create one coordinator class that implements `Agent` directly.
3. Register only the coordinator in `AgentRegistry` with allowed MCP servers.
4. In coordinator `run()`, call specialists in stages and pass each stage output to the next.
5. Keep coordinator logic explicit in Python (handoff format, retries, branch rules).
6. Add unit tests that assert call order and stage-to-stage context propagation.
=======
```bash
# 📋 List all registered agents
bin/agent.sh list
>>>>>>> theirs

<<<<<<< ours
        # Stage 2: Second specialist
        specialist2 = Specialist2Agent()
        result2 = await specialist2.run(result1)

        return result2

    def get_tools(self):
        return []
```
||||||| ancestor
This is the same pattern used by `travel-coordinator` and scales to routers, supervisors, and team-of-agents designs.
=======
# 🕵️ Get detailed info about what an agent can do
bin/agent.sh info developer
>>>>>>> theirs

<<<<<<< ours
After creating your agent in `src/agentic_framework/core/`, it automatically becomes available:
||||||| ancestor
After adding the file under `src/agentic_framework/core/`, the CLI command appears automatically:
=======
# 🚀 Run an agent with input
bin/agent.sh developer -i "Analyze the architecture of this project"

# ⏱️ Run with an execution timeout (seconds)
bin/agent.sh developer -i "Refactor this module" -t 120

# 📝 Run with debug-level verbosity
bin/agent.sh developer -i "Hello" -v
```

---

## 🧑‍💻 Local Development

Prefer running without Docker? We got you.

<details>
<summary><strong>System Requirements & Setup</strong></summary>

**Requirements:**
- Python 3.12+
- `ripgrep`, `fd`, `fzf`
>>>>>>> theirs

```bash
<<<<<<< ours
uv --directory agentic-framework run agentic-run my-agent -i "hello"
||||||| ancestor
uv --project agentic-framework run agentic-run my-agent -i "hello"
=======
# Install dependencies (blazingly fast with uv ⚡)
make install

# Run the test suite
make test

# Run agents directly in your environment
uv --directory agentic-framework run agentic-run developer -i "Hello"
>>>>>>> theirs
```
</details>

<details>
<summary><strong>Useful `make` Commands</strong></summary>

```bash
make install    # Install dependencies with uv
make test       # Run pytest with coverage
make format     # Auto-format codebase with ruff
make check      # Strict linting (mypy + ruff)
```
</details>

---

<<<<<<< ours
---
||||||| ancestor
=======
## 🤝 Contributing
>>>>>>> theirs

<<<<<<< ours
## Architecture
||||||| ancestor
## Scaling to Coordinators and Multi-Agent Systems
=======
We love contributions! Check out our [AGENTS.md](AGENTS.md) for development guidelines.
>>>>>>> theirs

<<<<<<< ours
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

---
||||||| ancestor
Recommended approach:
=======
**The Golden Rules:**
1. `make check` should pass without complaints.
2. `make test` should stay green.
3. Don't drop test coverage (we like our 80% mark!).
>>>>>>> theirs

<<<<<<< ours
## Development
||||||| ancestor
1. Build each specialist as a small `LangGraphMCPAgent` subclass.
2. Keep MCP permissions strict per specialist in the registry.
3. Add a coordinator agent that routes user intent to specialists.
4. Keep shared policies/prompts in one place; keep specialist prompts focused.
5. Add contract tests for routing and handoff behavior.
=======
---
>>>>>>> theirs

<<<<<<< ours
For contributing to the framework itself, see [AGENTS.md](AGENTS.md).

```bash
make install    # Install dependencies
make test       # Run tests (coverage threshold: 60%)
make format     # Auto-format code
make check      # Run all checks (lint + format check)
```
||||||| ancestor
This keeps the code easy for medium-level engineers to extend while remaining production-friendly.
=======
## 📄 License
>>>>>>> theirs

<<<<<<< ours
**Before committing:** Run `make check && make test`
||||||| ancestor
## Development Commands
=======
This project is licensed under the **MIT License**. See [LICENSE](LICENSE) for details.
>>>>>>> theirs

---

<<<<<<< ours
## License
||||||| ancestor
### Docker
- `make docker-build`: build Docker image
- `make docker-clean`: remove containers and images
- `bin/agent.sh <agent> [args]`: run agents in Docker (see [DOCKER.md](DOCKER.md))
=======
<p align="center">
  <strong>Stand on the shoulders of giants:</strong><br><br>
  <a href="https://python.langchain.com/"><img src="https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white" alt="LangChain"></a>
  <a href="https://modelcontextprotocol.io/"><img src="https://img.shields.io/badge/MCP-Protocol-4B32C3?style=for-the-badge" alt="MCP"></a>
  <a href="https://github.com/langchain-ai/langgraph"><img src="https://img.shields.io/badge/LangGraph-FF0000?style=for-the-badge" alt="LangGraph"></a>
</p>
>>>>>>> theirs

<<<<<<< ours
MIT License - see [LICENSE](LICENSE) for details.
||||||| ancestor
See `make help` for all available commands.
=======
<p align="center">
  If you find this useful, please consider giving it a ⭐!<br><br>
  <a href="https://github.com/jeancsil/agentic-framework/stargazers">
    <img src="https://img.shields.io/github/stars/jeancsil/agentic-framework?style=social&size=large" alt="Star the repo">
  </a>
</p>
>>>>>>> theirs
