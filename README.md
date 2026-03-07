# Duke Strategies Plugin Marketplace

Private marketplace for Duke Strategies Claude Code plugins.

## For end users

### First-time setup

```bash
# 1. Add the marketplace (one-time)
/plugin marketplace add stromy-org/duke-strategies-marketplace

# 2. Install the plugin
/plugin install duke-strategies

# 3. Install dependencies (one-time, in the plugin cache)
cd ~/.claude/plugins/cache/duke-strategies
npm install
uv sync
```

### Updating

```bash
/plugin update duke-strategies
```

Or pull manually:
```bash
cd ~/.claude/plugins/cache/duke-strategies
git pull && npm install && uv sync
```

### Usage

Once installed, skills are available in any Claude Code session:

| Skill | Command |
|-------|---------|
| PDF | `/duke-strategies:pdf` |
| Presentations | `/duke-strategies:pptx` |
| Documents | `/duke-strategies:docx` |
| Spreadsheets | `/duke-strategies:xlsx` |
| Proposals | `/duke-strategies:proposal` |
| Videos | `/duke-strategies:remotion-video` |

### Prerequisites

- Claude Code v2.1.49+
- Node.js 18+
- Python 3.11+ with [uv](https://docs.astral.sh/uv/)
- GitHub access to `stromy-org/duke-strategies-plugin` (private repo)
