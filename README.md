# Duke Strategies Plugin Marketplace

Public marketplace for Duke Strategies Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |
| Node.js | 18+ | PPTX, DOCX, Remotion skills |
| Python | 3.11+ | PDF, XLSX skills |
| [uv](https://docs.astral.sh/uv/) | latest | Python dependency manager |

## Installation

### Option A: From the Cowork Desktop UI

1. Open **Customize** → **Browse plugins** → **Personal** tab
2. Click the `+` to add a marketplace → enter `stromy-org/duke-strategies-marketplace`
3. Click **Duke strategies** → Install

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/duke-strategies-marketplace

# Install plugin
claude plugin install duke-strategies@duke-strategies-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/duke-strategies-marketplace/duke-strategies/0.1.0
npm install
uv sync
```

## Where skills work

| Interface | Skills available? | Notes |
|-----------|:-:|-------|
| **Claude Code CLI** | Yes | Terminal — full plugin support |
| **Desktop app — Code tab** | Yes | Same runtime as CLI |
| **Desktop app — Cowork tab** | Pending | Cowork plugin loading for marketplace plugins is a known limitation; expected to be resolved |

## Available skills

| Skill | Command |
|-------|---------|
| PDF | `/duke-strategies:pdf` |
| Presentations | `/duke-strategies:pptx` |
| Documents | `/duke-strategies:docx` |
| Spreadsheets | `/duke-strategies:xlsx` |
| Proposals | `/duke-strategies:proposal` |
| Videos | `/duke-strategies:remotion-video` |

## Updating

```bash
claude plugin update duke-strategies@duke-strategies-marketplace
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" | Ensure you have internet access; try CLI install (Option B) |
| Skills don't appear | Start a new session; ensure you're in the **Code** tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/duke-strategies-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`duke-strategies-plugin`): public — contains skills, brand data, company info
- **MCP server** (`dukestrategies-mcp`): tools and functions for strategy analysis
- **Strategy**: Plugin delivers skills (procedural knowledge); MCP delivers tools (callable functions)
- **Source format**: `marketplace.json` uses `"source": "url"` with a full `.git` URL
