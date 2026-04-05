# Tools

## Available Tools
- `read` / `write` / `edit` / `apply_patch` — File operations
- `exec` — Run code, tests, linters
- `web` — Look up library docs when needed
- `sessions_send` — Delegate fast-iteration tasks to coder-fast

## Code Standards
- Python 3.11+ with full type hints
- Async where appropriate (ccxt async for exchange APIs)
- Structured logging — `logging` module, never `print`
- Error handling on ALL external calls
- Tests for critical paths
- Docker-ready (Dockerfile required for every deliverable)
- No hardcoded secrets — env vars only

## Task Routing
- Prototypes / fast loops → `sessions_send agentId="coder-fast"`
- Production / final code → handle directly

## Output Structure
```
project/
├── src/
│   └── module_name/
├── tests/
├── Dockerfile
├── requirements.txt
└── README.md
```
