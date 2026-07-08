# Duke Strategies Plugin Marketplace

Public marketplace for Duke Strategies Claude Code plugins.

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |

## Installation

### Option A: From the Cowork Desktop UI

1. Open **Customize** → **Browse plugins** → **Personal** tab
2. Click the `+` to add a marketplace → enter `stromy-org/duke-strategies-marketplace`
3. Click **Duke Strategies** → Install

### Option B: From the CLI

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/duke-strategies-marketplace

# Install plugin
claude plugin install duke-strategies-plugin@duke-strategies-marketplace
```

### Post-install: dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/duke-strategies-marketplace/duke-strategies-plugin/0.1.0
npm install   # if the plugin has Node dependencies
uv sync       # if the plugin has Python dependencies
```

## Where skills work

| Interface | Skills available? | Notes |
|-----------|:-:|-------|
| **Claude Code CLI** | Yes | Terminal — full plugin support |
| **Desktop app — Code tab** | Yes | Same runtime as CLI |
| **Desktop app — Cowork tab** | Pending | Cowork plugin loading for marketplace plugins is a known limitation |

## Available skills

<!-- Update this table after adding skills to the plugin -->
| Skill | Command |
|-------|---------|
| _example_ | `/duke-strategies-plugin:example` |

## Updating

```bash
claude plugin update duke-strategies-plugin@duke-strategies-marketplace
```

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" with `Permission denied (publickey)` | Confirm the plugin entry uses an explicit `https://...git` URL, not the `github` shorthand |
| Other "Failed to install plugin" errors | Check `~/Library/Logs/Claude/main.log`; then try CLI install (Option B) |
| Skills don't appear | Start a new session; ensure you're in the **Code** tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/duke-strategies-marketplace` first |

## Architecture

- **Marketplace** (this repo): public — hosts `marketplace.json` only
- **Plugin** (`duke-strategies-plugin`): public — contains skills, brand data, company info
- **Source format**: use `"source": "url"` with an explicit HTTPS clone URL ending in `.git`, for example `https://github.com/stromy-org/duke-strategies-plugin.git`
- **Why not `github` shorthand?** Anthropic supports it, but Claude Code can resolve it to SSH (`git@github.com:...`) and fail on machines without a configured GitHub SSH key. Explicit HTTPS is the org portability standard.
