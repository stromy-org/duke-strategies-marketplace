# Duke Strategies Plugin Marketplace

Public marketplace pointing to the Duke Strategies Claude Code plugin (private repo).

## Prerequisites

| Requirement | Version | Why |
|-------------|---------|-----|
| Claude Code | v2.1.49+ | Plugin runtime (CLI or Desktop Code tab) |
| Node.js | 18+ | PPTX, DOCX, Remotion skills |
| Python | 3.11+ | PDF, XLSX skills |
| [uv](https://docs.astral.sh/uv/) | latest | Python dependency manager |
| [GitHub CLI](https://cli.github.com/) | latest | Authentication for private plugin repo |
| GitHub access | — | Collaborator on `stromy-org/duke-strategies-plugin` (private) |

## First-time setup

### Step 0 — Authenticate GitHub (required — plugin repo is private)

Claude Code needs a GitHub token to clone the private plugin repo during installation.

```bash
# 1. Authenticate with GitHub CLI (if not already)
gh auth login

# 2. Add token export to your shell profile
echo 'export GITHUB_TOKEN=$(gh auth token)' >> ~/.zshrc
source ~/.zshrc

# 3. Verify
echo $GITHUB_TOKEN   # should print a token
```

### Step 1 — Add the marketplace and install (CLI only)

Installation **must** be done from the terminal (Claude Code CLI), not from the Cowork desktop UI. The Cowork "Browse plugins" UI runs in a sandboxed VM that cannot access private GitHub repos.

```bash
# Add marketplace (one-time)
claude plugin marketplace add stromy-org/duke-strategies-marketplace

# Install plugin
claude plugin install duke-strategies@duke-strategies-marketplace
```

### Step 2 — Install dependencies (one-time)

```bash
cd ~/.claude/plugins/cache/duke-strategies-marketplace/duke-strategies/0.1.0
npm install
uv sync
```

### Step 3 — Use skills

Skills are available in the **Code tab** of the Claude Desktop app, or in the CLI:

```
/duke-strategies:proposal
/duke-strategies:pdf
```

> **Important:** Skills appear in the **Code** tab, not the Cowork tab. Cowork (task mode) is a different runtime that does not load Claude Code plugins.

## Updating

```bash
claude plugin update duke-strategies@duke-strategies-marketplace
```

Then re-install dependencies if they changed:

```bash
cd ~/.claude/plugins/cache/duke-strategies-marketplace/duke-strategies/0.1.0
npm install && uv sync
```

## Available skills

| Skill | Command |
|-------|---------|
| PDF | `/duke-strategies:pdf` |
| Presentations | `/duke-strategies:pptx` |
| Documents | `/duke-strategies:docx` |
| Spreadsheets | `/duke-strategies:xlsx` |
| Proposals | `/duke-strategies:proposal` |
| Videos | `/duke-strategies:remotion-video` |

## Troubleshooting

| Problem | Fix |
|---------|-----|
| "Failed to install plugin" from CLI | Run `echo $GITHUB_TOKEN` — if empty, follow Step 0 |
| "Failed to install plugin" from Cowork UI | Expected — use the CLI instead (Step 1). The Cowork VM cannot access private repos |
| Plugin installs but skills don't appear | Make sure you're in the **Code** tab, not Cowork tab |
| Dependency errors on first use | Run `npm install && uv sync` in the plugin cache dir |
| Token expired | Run `gh auth refresh` then `source ~/.zshrc` |
| "Plugin not found in marketplace" | Run `claude plugin marketplace add stromy-org/duke-strategies-marketplace` first |

## Architecture notes

- **Marketplace repo** (this repo): public — hosts `marketplace.json` only
- **Plugin repo** (`duke-strategies-plugin`): private — contains skills, brand data, company info
- **Source format**: `marketplace.json` uses `"source": "url"` with a full `.git` URL (not `"source": "github"` which is not a recognized format)
- **Cowork limitation**: The Cowork desktop app runs plugin installs inside a sandboxed Linux VM. Host credentials (`GITHUB_TOKEN`, SSH keys, git credential helpers) are not available inside the VM. This is by design for security. Install via CLI instead.
