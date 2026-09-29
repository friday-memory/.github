<div align="center">

<img src="https://raw.githubusercontent.com/friday-memory/friday/main/docs/assets/banner.png" alt="Friday Memory - Persistent Cognitive Memory Layer for AI Coding Agents" width="100%" style="border-radius: 8px; border: 1px solid #1e293b;" />

<br><br>

# Friday Memory

**The open-source persistent cognitive substrate for AI coding agents.**

Persist architectural decisions, schemas, and invariants across developer sessions without prompt bloat.

<br>

<p align="center">
  <a href="https://github.com/friday-memory/friday/stargazers"><img src="https://img.shields.io/github/stars/friday-memory/friday?style=flat&color=334155&label=Stars" alt="GitHub Stars"/></a>
  <a href="https://github.com/friday-memory/friday/network/members"><img src="https://img.shields.io/github/forks/friday-memory/friday?style=flat&color=334155&label=Forks" alt="GitHub Forks"/></a>
  <a href="https://pypi.org/project/friday-memory/"><img src="https://img.shields.io/pypi/v/friday-memory?style=flat&color=334155&label=PyPI" alt="PyPI Package"/></a>
  <a href="https://github.com/friday-memory/friday/releases"><img src="https://img.shields.io/badge/release-v1.4.5-334155?style=flat" alt="Release"/></a>
  <a href="https://github.com/friday-memory/friday/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-334155?style=flat" alt="MIT License"/></a>
  <a href="https://modelcontextprotocol.io"><img src="https://img.shields.io/badge/protocol-MCP_2024--11--05-334155?style=flat" alt="MCP Protocol"/></a>
</p>

</div>

---

## Overview

AI coding agents (Cursor, Claude Code, Windsurf, GitHub Copilot, Antigravity, Aider) operate within fixed context windows. When engineering projects scale, developers attempt to manage state by bloating `.cursorrules`, `AGENTS.md`, or system prompts. 

This causes two systemic failures:
1. **Prompt Bloat & Token Degradation**: Burning thousands of tokens per turn on rules that are 90% irrelevant to the current diff.
2. **State Drift & Hallucination**: Outdated constraints linger in static markdown files, causing models to hallucinate contradictory architectures.

**Friday Memory** resolves this by providing a self-hosted, decoupled cognitive memory substrate over the **Model Context Protocol (MCP)**. Instead of stuffing prompts, agents access on-demand ground truth through standardized tool primitives.

---

## Ecosystem

| Component | Repository / Package | Description |
| :--- | :--- | :--- |
| **Friday Core Substrate** | [`friday-memory/friday`](https://github.com/friday-memory/friday) | Self-hosted FastAPI gateway, Mem0 episodic memory, ChromaDB vector store, and Neo4j knowledge graph. |
| **Python SDK & CLI** | [`friday-memory` on PyPI](https://pypi.org/project/friday-memory/) | Official synchronous & asynchronous Python SDK client, LangChain integration, and multi-agent rule generator CLI. |
| **Model Context Protocol (MCP)** | Integrated in [`mcp/server.py`](https://github.com/friday-memory/friday/tree/main/mcp) | Native stdio MCP server exposing `get_context`, `memory_search`, `get_blast_radius`, and `add_fact`. |
| **Neural Studio** | Integrated in [`studio/`](https://github.com/friday-memory/friday/tree/main/studio) | Three.js interactive 3D knowledge graph visualizer with live force-directed topology. |

---

## Core Architecture

```
[ Developer / AI Coding Agent ]
           │
           │ MCP (stdio) / REST API
           ▼
┌────────────────────────────────────────────────────────┐
│             Friday Gateway (FastAPI)                   │
├────────────────────────────────────────────────────────┤
│ Layer 1: Core System & Developer Cognitive Calibration │
│ Layer 2: Versioned Facts Ledger (Auto-Supersede)       │
│ Layer 3: Semantic Vector Retrieval (ChromaDB / Mem0)   │
│ Layer 4: Multi-Hop Knowledge Graph (Neo4j)             │
└────────────────────────────────────────────────────────┘
```

### Key Architectural Capabilities

- **Two-Way Zero-Amnesia Protocol**: Standardized **Read Gate** (pull ground truth before planning) and **Write Gate** (record verified decisions upon task completion).
- **Multi-Hop Graph Blast-Radius Traversal**: Evaluate transitive downstream impacts across microservices and schemas up to 4 hops away before executing breaking refactors (`get_blast_radius`).
- **Deterministic Key-Collision Auto-Supersede**: Updates to existing key-value facts (`Key: Value`) automatically supersede older entries within the same project namespace, eliminating prompt conflicts.
- **Universal Agent Rule Engine**: CLI tool to generate minimal, zero-bloat rule files for 8 major agent environments (`friday rules generate --all`).

---

## Quickstart

### 1. Install the SDK & CLI
```bash
pip install --upgrade friday-memory
```

### 2. Generate Lean Rule Files for Your Project
```bash
# Generate rules for Cursor, Claude, Gemini, Copilot, Windsurf, Aider, and Continue
friday rules generate --all --project "MyProject"
```

### 3. Connect via MCP
Add to your IDE's MCP configuration (Cursor, Claude Desktop, Antigravity, VS Code):
```json
{
  "mcpServers": {
    "friday": {
      "command": "python",
      "args": ["-m", "mcp.server"],
      "env": {
        "FRIDAY_URL": "http://localhost:8000",
        "BRAIN_API_KEY": "your_secret_key"
      }
    }
  }
}
```

---

## Community & Contributing

Friday Memory is an open-source initiative dedicated to reliable, transparent, and self-hosted developer intelligence. We welcome code contributions, issue reports, and architectural proposals.

- **Main Repository**: [github.com/friday-memory/friday](https://github.com/friday-memory/friday)
- **Contributing Guidelines**: [CONTRIBUTING.md](https://github.com/friday-memory/friday/blob/main/CONTRIBUTING.md)
- **Code of Conduct**: [CODE_OF_CONDUCT.md](https://github.com/friday-memory/friday/blob/main/CODE_OF_CONDUCT.md)
- **Security Policy**: [SECURITY.md](https://github.com/friday-memory/friday/blob/main/SECURITY.md)

---

<div align="center">
  <sub>Maintained by the Friday Memory Open-Source Community. Released under the MIT License.</sub>
</div>
