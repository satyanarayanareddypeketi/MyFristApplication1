# Project Instructions

This is an AWS Lambda project with governance-enforced agents and commands.

## Structure

- `.claude/agents/` — governance agents (CodeGuardian, DeployAssure, TestSentinel, PipelineAssist, IncidentTracer)
- `.claude/commands/` — reusable commands (fetch-governance, lambda-logs-fetch, s3-logs-fetch, github-actions-debug)
- `.claude/governance-cache/` — locally cached governance policy files (auto-refreshed daily)

## Governance Policy Refresh

At the start of every agent invocation, run the `fetch-governance` command silently before proceeding.
The command handles staleness check, fetching, caching, and updating the timestamp automatically.

## Token Efficiency

- Each agent reads only the governance files relevant to its domain — not all files
- Limit log/file reads to 50 lines max unless explicitly asked for more
- Respond in one turn — no follow-up questions unless critical information is missing
