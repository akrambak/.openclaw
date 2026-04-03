---
name: openclaw-agent-spawn
description: Creates a new OpenClaw agent — workspace directory, AGENTS.md, SOUL.md, and openclaw.json registration. Use when the user wants to add a new specialized agent to the OpenClaw system, create a new role, or expand agent capabilities.
---

# OpenClaw Agent Spawn

## Steps

1. **Choose agent ID** — lowercase, no spaces (e.g. `analyst`, `writer`, `scraper`)
2. **Decide model** — local Ollama ID or Anthropic model ID
3. **Create workspace**
4. **Register in openclaw.json**
5. **Validate config**

## Create Workspace

```bash
AGENT_ID="your-agent-id"
BASE="/home/ultra9-ubuntu/.openclaw"
mkdir -p "$BASE/workspace-$AGENT_ID"
```

## Required Files

### AGENTS.md
```markdown
# AGENTS.md — {Role Name}

## System Role
[One sentence describing this agent's function]

## Workflow Position
[Where in REQUEST → orchestor → ... → DEPLOYED this agent fits]

## Inputs / Outputs
- Input: [what it receives from previous agent]
- Output: [what it sends to next agent]

## Agent Registry
[Copy from orchestor AGENTS.md]
```

### SOUL.md
```markdown
# SOUL.md — {Role Name}

## Identity
[Terse: what this agent IS, not what it does]

## Primary Directive
[Single sentence mission]

## Decision Framework
[How it chooses between approaches]

## Boundaries
[What it will NOT do]
```

## Register in openclaw.json

Add to the `agents` array:
```json
{
  "id": "your-agent-id",
  "workspace": "/home/ultra9-ubuntu/.openclaw/workspace-your-agent-id",
  "model": "qwen2.5-coder:32b",
  "identity": {
    "name": "YourAgent",
    "emoji": "🎯"
  }
}
```

Also add to `tools.agentToAgent.allowlist` if it needs to receive messages from other agents.

## Validate

```bash
python3 -c "import json; json.load(open('openclaw.json')); print('OK')"
```

## Initialize Git (optional)
```bash
cd workspace-$AGENT_ID && git init && git add . && git commit -m "init: $AGENT_ID workspace"
```
