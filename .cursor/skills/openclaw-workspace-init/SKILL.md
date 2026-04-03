---
name: openclaw-workspace-init
description: Initializes or repairs an OpenClaw agent workspace with all required files (AGENTS.md, SOUL.md, MEMORY.md, workspace-state.json). Use when a workspace is missing files, a new workspace was created without scaffolding, or when setting up workspace-cto/workspace-coder/workspace-coder-fast which currently only have SOUL.md.
---

# OpenClaw Workspace Init

## Check What's Missing

```bash
WORKSPACE="/home/ultra9-ubuntu/.openclaw/workspace-AGENTID"
for f in AGENTS.md SOUL.md MEMORY.md; do
  [ -f "$WORKSPACE/$f" ] || echo "MISSING: $f"
done
[ -f "$WORKSPACE/.openclaw/workspace-state.json" ] || echo "MISSING: .openclaw/workspace-state.json"
```

## Minimum Viable Workspace

Create these files if missing:

### MEMORY.md
```markdown
# Persistent Memory

## Rules
- [Add permanent rules here that survive across sessions]

## Decisions
- [Key architectural or operational decisions]

## Context
- [Permanent context this agent always needs]
```

### .openclaw/workspace-state.json
```json
{
  "version": "1.0",
  "agent": "AGENT_ID",
  "initialized": "YYYY-MM-DD",
  "status": "active"
}
```

## Incomplete Workspaces to Fix Now

These currently only have SOUL.md and need full initialization:
- `workspace-cto/` — CTO architecture agent
- `workspace-coder/` — Production coder agent  
- `workspace-coder-fast/` — Fast iteration coder

For each, create AGENTS.md referencing the main agent registry in `workspace-orchestor/AGENTS.md`.

## Git Setup (if workspace has .git)
```bash
cd $WORKSPACE
git status  # check state
git log --oneline -5  # check history
```

If no git: `git init && git add . && git commit -m "init: workspace scaffold"`
