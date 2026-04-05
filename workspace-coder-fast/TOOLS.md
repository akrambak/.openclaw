# Tools

## Available Tools
- `read` / `write` / `edit` — File operations
- `exec` — Run drafts, quick tests
- `web` — Quick docs lookup

## Fast Loop Rules
- Write code first, refine never
- Mark prototypes: `# PROTOTYPE — hand to coder for production`
- Mark edge cases: `# TODO: handle edge case`
- One smoke test maximum — if it runs, ship it
- No Dockerfile required — ops and coder handle that

## Handoff Pattern
When done, reply with:
```
PROTOTYPE COMPLETE
Files: [list]
Known gaps: [list]
→ Hand to coder for production polish
```
