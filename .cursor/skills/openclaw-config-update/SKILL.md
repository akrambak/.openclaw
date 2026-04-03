---
name: openclaw-config-update
description: Safely reads and updates openclaw.json — the central OpenClaw config. Use when changing models, adding/removing agents, updating channel configs, modifying gateway settings, or toggling plugins. Prevents config corruption and token leaks.
---

# OpenClaw Config Update

## Pre-Edit Checklist
- [ ] Backup exists: `cp openclaw.json openclaw.json.bak`
- [ ] Know the exact key path to modify
- [ ] Have the new value ready

## Read Current Value (safe — no secrets printed)

```bash
# List all agents
python3 -c "
import json
c = json.load(open('openclaw.json'))
for a in c['agents']:
    print(a['id'], '-', a.get('model','?'), '-', a['identity']['name'])
"

# List active plugins
python3 -c "
import json
c = json.load(open('openclaw.json'))
for k,v in c.get('plugins',{}).items():
    print(k, v.get('enabled'))
"
```

## Common Update Patterns

### Change agent model
```python
import json
with open('openclaw.json') as f:
    c = json.load(f)

agent = next(a for a in c['agents'] if a['id'] == 'TARGET_AGENT_ID')
agent['model'] = 'NEW_MODEL_ID'

with open('openclaw.json', 'w') as f:
    json.dump(c, f, indent=2)
print("Updated")
```

### Add model to Ollama profile
```python
import json
with open('openclaw.json') as f:
    c = json.load(f)

ollama_profile = next(p for p in c['auth']['profiles'] if p['provider'] == 'ollama')
ollama_profile['models'].append('new-model:tag')

with open('openclaw.json', 'w') as f:
    json.dump(c, f, indent=2)
```

### Enable a plugin
```python
import json
with open('openclaw.json') as f:
    c = json.load(f)
c['plugins']['PLUGIN_NAME']['enabled'] = True
with open('openclaw.json', 'w') as f:
    json.dump(c, f, indent=2)
```

## Validate After Edit

```bash
python3 -c "import json; json.load(open('openclaw.json')); print('OK')"
```

## Rollback If Needed

```bash
cp openclaw.json.bak openclaw.json
```

## Never Edit Directly
- Do NOT use `sed` or text editors that might corrupt JSON
- Do NOT print token/auth values during editing
- Backups auto-exist at `openclaw.json.bak` through `.bak.4` — check before overwriting
