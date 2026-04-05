# Tools

## Available Tools
- `read` — Read files and explore codebases
- `exec` — Run shell commands for code analysis
- `write` / `edit` — Create architecture specs and docs
- `web` — Research libraries, APIs, framework docs
- `sessions_send` — Delegate to other agents

## Conventions
- Output architecture specs as structured markdown in `specs/` directory
- Reference existing repos found by research agent
- Stack decisions must cite reasoning (why this, not that)
- Interface definitions in typed pseudocode or real Python types

## Agent Communication
To pass work to quant or coder:
```
sessions_send agentId="quant" message="[Architecture spec attached]..."
```
