---
name: openclaw-pipeline-debug
description: Diagnoses and fixes issues in the OpenClaw multi-agent pipeline — broken agent routing, failed handoffs, model errors, gateway issues, channel disconnections. Use when agents aren't responding, the pipeline stalls, or messages aren't routing correctly.
---

# OpenClaw Pipeline Debug

## Quick Diagnostics Checklist

```bash
BASE="/home/ultra9-ubuntu/.openclaw"

# 1. Is Ollama running?
curl -s http://127.0.0.1:11434/api/tags | python3 -m json.tool | head -20

# 2. Is the gateway alive?
curl -s http://127.0.0.1:18789/health 2>/dev/null || echo "Gateway DOWN"

# 3. Config valid?
python3 -c "import json; json.load(open('$BASE/openclaw.json')); print('Config OK')"

# 4. Recent errors?
tail -50 $BASE/logs/config-audit.jsonl
```

## Common Issues & Fixes

### Agent Not Responding
1. Check model is loaded: `curl http://127.0.0.1:11434/api/tags | grep MODEL_ID`
2. Check workspace path exists: `ls workspace-AGENTID/`
3. Check agent is in `openclaw.json agents[]`
4. Check agent is in `tools.agentToAgent.allowlist`

### Pipeline Stalls After Research
Most likely: `cto` workspace missing AGENTS.md. Run `openclaw-workspace-init` skill.

### Gateway 401 Errors
Token mismatch. Compare `gateway.token` in `openclaw.json` with `GATEWAY_TOKEN` in `.env` (if set).

### Channel Disconnection (Discord/Slack/Telegram)
1. Check token in `openclaw.json channels.{platform}.token`
2. Verify bot permissions / channel allowlist
3. Check network connectivity from WSL2: `curl -s https://discord.com/api/gateway`

### Model OOM / Slow Response
1. Check Ollama memory: `ollama ps`
2. Unload unused models: `ollama stop MODEL_ID`
3. For heavy models, ensure Q4_K_M quantization is used

## Session Inspection

```bash
# Last session for main agent
ls -lt $BASE/agents/main/sessions/*.jsonl | head -3
tail -100 $BASE/agents/main/sessions/LATEST.jsonl
```

## Log Levels

Increase verbosity in `.env`:
```
OPENCLAW_LOG_LEVEL=debug
```

## Escalation Path
If debug fails → escalate to orchestor (Claude) with full error context.
