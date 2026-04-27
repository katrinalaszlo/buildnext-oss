# BuildNext

Turn raw customer signal into evidence-grounded user stories. No database, no hosting — just markdown and an LLM.

## How it works

BuildNext is a Karpathy-style LLM wiki for product development. You give it raw customer signal (call transcripts, support tickets, notes). An AI agent reads, extracts, and synthesizes it into a structured knowledge base you can browse in Obsidian or query from any agent.

```
raw/              # paste transcripts here (input)
wiki/             # agent-maintained output
  customers/      # one page per customer, extracted quotes
  stories/        # synthesized user stories
  features/       # story groupings
  index.md        # catalog of all pages
  log.md          # what changed and when
CLAUDE.md         # schema — rules for how the agent operates
config.md         # internal speakers to filter, evidence tags
```

Three layers: **raw** (immutable input), **wiki** (LLM-maintained output), **schema** (rules).

## Prerequisites

- Git
- An AI coding tool that reads `CLAUDE.md` — [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Cursor](https://cursor.sh), [Codex](https://openai.com/index/codex/), or similar
- (Optional) [Obsidian](https://obsidian.md) for graph view and backlinks

## Quick start

1. Clone the repo
   ```bash
   git clone https://github.com/katrinalaszlo/buildnext-oss.git
   cd buildnext-oss
   ```

2. Copy config and add your team's names
   ```bash
   cp config.example.md config.md
   ```
   Edit `config.md` — replace the placeholder names with your team members so the agent skips their quotes during ingestion.

3. Drop a transcript into `raw/`, or use the included example (`raw/example-transcript.md`)

4. Open the project in your AI editor and tell it: **"Ingest the transcript in raw/"**

5. Open the `wiki/` folder (not the repo root) in [Obsidian](https://obsidian.md) as a vault. You'll see a graph of customers, stories, and features — all linked. No Obsidian? The files are plain markdown, readable in any editor.

## What the agent does

- **Ingest** — reads raw transcripts, extracts quotes, creates/updates customer pages
- **Synthesize** — finds recurring themes across customers, generates user stories with acceptance criteria
- **Lint** — finds orphan evidence, weak stories, missing links
- **Query** — answers questions about your evidence base with citations

Every story traces back to what customers actually said. No evidence, no story.

## Browsing the wiki

Download [Obsidian](https://obsidian.md) (free) and open the `wiki/` folder as a vault. You get:

- **Graph view** — see how customers, stories, and features connect
- **Backlinks** — click any customer to see every story they're cited in
- **Search** — full-text across all your evidence

Or just read the markdown files in any editor — they're plain text with `[[wikilinks]]`.

## You're in control

The wiki is just markdown. Edit any file and the agent respects your changes:

- **Delete a story** the agent got wrong — it won't regenerate it
- **Move a story** to a different feature — the agent learns the correct grouping
- **Reword acceptance criteria** — the agent follows your style going forward
- **Add notes or context** — the agent preserves them in future updates

Every edit you make teaches the agent what "good" looks like for your project. The wiki gets smarter over time.

## Connecting external sources (optional)

BuildNext can optionally pull data from external sources via MCP. This requires API keys for whatever service you connect.

```bash
cp .mcp.json.example .mcp.json
```

Add your API keys to `.mcp.json`, then tell the agent: "Pull transcripts from Airtable and ingest them."

The agent reads from the source via MCP, writes records to `raw/`, and runs the ingest workflow. Add any MCP server to connect more sources — Notion, Google Drive, Slack, Gong, etc.

Not required for basic usage. Pasting transcripts directly into `raw/` works fine.

## Agent access

Any agent that reads `CLAUDE.md` (Claude Code, Cursor, Codex) can operate on the wiki. The schema defines the workflows, page formats, and rules.

For MCP-compatible agents, the wiki is readable as-is — the agent reads markdown files from the filesystem.

## Example

The repo ships with 3 fictional transcripts and a pre-built wiki (3 customers, 2 stories, 2 features) so you can explore the output immediately. Open `wiki/` in Obsidian to see the graph.

When you're ready to use your own data, just drop transcripts into `raw/` and ingest. Your data lives alongside the examples. Delete the example files whenever you want — they won't affect your wiki.

## License

MIT
