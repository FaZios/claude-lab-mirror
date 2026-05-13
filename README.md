# claude-lab-mirror

Auto-published, sanitised slices of Fazio Lab audit state.

**Source**: `claude-config` repo private. This is a daily-synced subset for
Claude Web second-opinion context priming. Not the source of truth.

See [ADR-0004](https://github.com/FaZios/claude-config/blob/main/docs/adr/0004-bridge-cli-web.md)
for the contract.

## What's here

- `audit/` — top-level Fazio Lab audit files (NORTH-STAR, master plan, digest, latest baselines)
- `projects/` — per-project dashboards (DASHBOARD.md slices)

## What's NOT here

- Session handoffs, OPS-LOG, harvest findings (private).
- Any file containing PATs, IPs, hostnames, paths, or LLM API keys (sanitiser filtered).
