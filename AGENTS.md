# Agent Setup

BuildNext is an agent-operated evidence wiki. The schema and all workflows are defined in `CLAUDE.md`.

## Claude Code

Open this directory in Claude Code. It reads `CLAUDE.md` automatically.

```
cd buildnext-oss
claude
```

## Cursor

Open this directory in Cursor. It reads `CLAUDE.md` automatically.

## Codex

```
codex exec "Ingest the transcript in raw/" -C .
```

## Any other agent

Point it at `CLAUDE.md`. It defines four workflows: ingest, synthesize, lint, query.

## External sources (optional)

Copy `.mcp.json.example` to `.mcp.json` and add API keys to pull from Airtable, Notion, Slack, etc. Not required for basic usage.
