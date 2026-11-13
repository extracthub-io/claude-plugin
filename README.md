# ExtractHub plugin for Claude Code

Build, test and release [ExtractHub](https://extracthub.io) extractors (versioned web scrapers that turn a page
type into structured JSON) and pipelines from Claude Code, and run them through the ExtractHub MCP server.

The plugin contains:
- **Skill `extracthub-extractor-builder`**: writes an extractor definition (request options + CSS / JSON field
  config) for a page type, checks it on the real page, uploads it, tests it and releases it when you agree.
- **Skill `extracthub-pipeline-builder`**: chains released extractors (a list page, then every detail page it
  links to) into one dataset, runs it and schedules it when you agree.
- **MCP server `extracthub`** (`https://api.extracthub.io/mcp`, Streamable HTTP): search and run extractors,
  batches, jobs and pipelines, and create, validate and release extractors.

## Install

```
/plugin marketplace add extracthub-io/claude-plugin
/plugin install extracthub@extracthub
```

## API key

The MCP server and the skills' validation script read your key from the `EXTRACTHUB_API_KEY` environment
variable. Create a key in the ExtractHub dashboard (API keys page), then put it in Claude Code's settings, for
example `~/.claude/settings.json` or a project's `.claude/settings.local.json` (keep it out of git):

```json
{ "env": { "EXTRACTHUB_API_KEY": "YOUR_EXTRACTHUB_API_KEY" } }
```

Restart Claude Code; `/mcp` should list `extracthub` as connected.

- A test key (`exth_test_...`) runs in the sandbox: no credit is used and no page is fetched. Creating,
  updating and releasing extractors and pipelines needs a live key.
- Requests through MCP have the same prices and limits as the REST API: https://extracthub.io/#pricing

## Without the plugin

The skills are also published on their own (clone into `~/.claude/skills/`):
- https://github.com/extracthub-io/extracthub-extractor-builder
- https://github.com/extracthub-io/extracthub-pipeline-builder

Other MCP clients: https://extracthub.io/mcp

## License

MIT
