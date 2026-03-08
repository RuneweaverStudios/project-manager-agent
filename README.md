# project-manager-agent

**OpenClaw skill: sub-agent monitoring, stall detection, and automated steering.**

Monitors active OpenClaw sub-agents, detects stalls and failures, provides status reports, and can automatically steer stuck agents via `sessions_send`.

## Features

- List and monitor all active sub-agents
- Detect stalled agents based on configurable time thresholds
- Identify agents that aborted their last run
- JSON output with stalled session keys for automated steering
- Cooldown tracking to prevent over-steering
- Configurable via `config.json`

## Install

```bash
clawhub install project-manager-agent
# or:
git clone https://github.com/RuneweaverStudios/project-manager-agent.git
cp -r project-manager-agent ~/.openclaw/workspace/skills/
```

## Quick start

```bash
# Human-readable status report
python3 scripts/project_manager.py

# JSON output for agent steering
python3 scripts/project_manager.py --json --staleness_threshold_minutes 10

# Record steered sessions (after calling sessions_send)
python3 scripts/project_manager.py --record-steered key1 key2
```

## Configuration

Edit `config.json` in the skill root:

```json
{
  "staleness_threshold_minutes": 10,
  "steer_cooldown_minutes": 15,
  "steer_message": "Please continue working on your task.",
  "max_steer_per_run": 5,
  "session_key_prefix": "agent:main:subagent:"
}
```

## Requirements

- Python 3.6+
- `OPENCLAW_HOME` environment variable (or default `~/.openclaw`)

## License

MIT
