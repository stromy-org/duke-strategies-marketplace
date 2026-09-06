# Duke Strategies Plugin Marketplace

Public marketplace for Duke Strategies Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude account with plugin access | — | Cowork / Claude for Work / Team (desktop or web), or Claude Code v2.1.49+ |

## Installation

### Option A: In the Claude app (Cowork, Claude for Work / Team)

1. Open **Settings → Plugins** (or **Connectors & plugins**)
2. **Add marketplace** → enter `stromy-org/duke-strategies-marketplace`
3. Click **Duke Strategies** → **Install**
4. Switch on the **stromy-format** and **nl-gov-data** connectors under **Settings → Connectors**, then say `/duke-strategies:getting-started` in a chat

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/duke-strategies-marketplace

# Install plugin
claude plugin install duke-strategies@duke-strategies-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/duke-strategies-marketplace/duke-strategies/<version>
npm install   # if the plugin has Node dependencies
uv sync       # if the plugin has Python dependencies
```

## Where skills work

| Interface | Skills available? | Notes |
|-----------|:-:|-------|
| **Claude app — Cowork, Claude for Work / Team** | Yes | Install via **Settings → Plugins**; connectors via **Settings → Connectors** |
| **Claude Code CLI** | Yes | Terminal — full plugin support |
| **Claude desktop — Code tab** | Yes | Same runtime as the CLI |

## Available skills

The plugin ships 41 skills, invoked as `/duke-strategies:<skill>` — the full table with one-line descriptions is in the [plugin README](https://github.com/stromy-org/duke-strategies-plugin#skills). Start with `/duke-strategies:getting-started`.

## Updating

```bash
claude plugin update duke-strategies@duke-strategies-marketplace
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" with `Permission denied (publickey)` | Confirm the plugin entry uses an explicit `https://...git` URL, not the `github` shorthand |
| Other "Failed to install plugin" errors | Check `~/Library/Logs/Claude/main.log`; then try CLI install (Option B) |
| Skills don't appear | Start a new chat; in the Claude app check **Settings → Plugins** shows the plugin as installed |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/duke-strategies-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`duke-strategies-plugin`): public — contains skills, brand data, company info
- **Source format**: use `"source": "url"` with an explicit HTTPS clone URL ending in `.git`, for example `https://github.com/stromy-org/duke-strategies-plugin.git`
- **Why not `github` shorthand?** Anthropic supports it, but Claude Code can resolve it to SSH (`git@github.com:...`) and fail on machines without a configured GitHub SSH key. Explicit HTTPS is the org portability standard.
