---
name: openclaw-self-improve-loop
description: Runs a structured self-improvement cycle on the OpenClaw system — audits rules/skills/MCPs, identifies gaps, implements improvements, and tracks compounding value. Use when the user wants to improve the system, add capabilities, reduce friction, or execute a self-improvement sprint.
---

# OpenClaw Self-Improvement Loop

## The Loop
```
AUDIT → IDENTIFY GAPS → PRIORITIZE → IMPLEMENT → VALIDATE → TRACK
```

## Phase 1: Audit Current State

```bash
BASE="/home/ultra9-ubuntu/.openclaw"
CURSOR_DIR="$BASE/.cursor"

echo "=== RULES ===" && ls $CURSOR_DIR/rules/ 2>/dev/null || echo "none"
echo "=== SKILLS ===" && ls $CURSOR_DIR/skills/ 2>/dev/null || echo "none"
echo "=== WORKSPACE STATUS ===" 
for ws in $BASE/workspace-*/; do
    agent=$(basename $ws | sed 's/workspace-//')
    missing=""
    [ -f "$ws/AGENTS.md" ] || missing="$missing AGENTS.md"
    [ -f "$ws/SOUL.md" ]   || missing="$missing SOUL.md"
    [ -f "$ws/MEMORY.md" ] || missing="$missing MEMORY.md"
    echo "$agent: ${missing:-OK}"
done
```

## Phase 2: Identify Gaps

Rate each area 1-5 (1=broken, 5=excellent):
- [ ] **Rules**: Do rules prevent repeated mistakes?
- [ ] **Skills**: Are workflows encoded and reusable?
- [ ] **MCPs**: Can agents access all tools they need?
- [ ] **Workspaces**: Are all agents fully initialized?
- [ ] **Memory**: Is valuable context persisting?
- [ ] **Pipeline**: Does REQUEST → DEPLOYED work end-to-end?

## Phase 3: Prioritize (Impact × Frequency)

Highest priority improvements:
1. Fix broken things first (score 1-2)
2. Add high-frequency missing tools (score 3)
3. Optimize high-cost operations last (score 4-5)

## Phase 4: Implement

For each improvement, choose type:
- **Rule** → `.cursor/rules/NAME.mdc`
- **Skill** → `.cursor/skills/NAME/SKILL.md`
- **Workspace file** → `workspace-AGENT/FILENAME.md`
- **Config change** → use `openclaw-config-update` skill
- **MCP** → install + register in Cursor settings

## Phase 5: Validate

```bash
# Rules loaded correctly?
ls -la .cursor/rules/*.mdc | wc -l

# Skills discoverable?
ls -la .cursor/skills/*/SKILL.md

# Config still valid?
python3 -c "import json; json.load(open('openclaw.json')); print('Config OK')"

# Test pipeline: send a simple request through main → orchestor
```

## Phase 6: Track

Append to `workspace-orchestor/IMPROVEMENT_BACKLOG.md`:
```markdown
## [DATE] Improvement Title
- Type: rule | skill | mcp | workspace | config
- Problem: [what was wrong/slow/missing]
- Solution: [what was built]
- Impact: [time saved / errors prevented / cost reduced]
- Status: done
```

## Current Known Gaps (Bootstrap)

| Gap | Type | Priority |
|-----|------|----------|
| workspace-cto missing AGENTS.md | workspace | HIGH |
| workspace-coder missing AGENTS.md | workspace | HIGH |
| workspace-coder-fast missing AGENTS.md | workspace | HIGH |
| No filesystem MCP | mcp | HIGH |
| No git MCP | mcp | MEDIUM |
| No sequential-thinking MCP | mcp | MEDIUM |
| No memory MCP | mcp | MEDIUM |
| IMPROVEMENT_BACKLOG.md doesn't exist yet | workspace | LOW |
