# ClawdNotes Template

A shareable Obsidian vault template designed for AI-assisted note-taking with Claude Code, OpenCode, Cursor, OpenClaw, and other AI coding assistants.

## What This Is

An opinionated, production-ready note-taking system that:
- Uses PARA organization (Projects, Areas, Resources, Archive)
- Integrates seamlessly with AI assistants
- Includes automation for daily briefings, inbox processing, and reviews
- Provides clear conventions that both humans and AI can follow

**Fork this, make it yours.**

## Quick Start

```bash
# Clone the template
git clone https://github.com/YOUR_USERNAME/clawdnotes-template ~/Notes

# Or use GitHub's template feature
# Click "Use this template" on GitHub

# Open in Obsidian
# File → Open Vault → Select the cloned folder
```

## Structure

```
.
├── 0-Inbox/           # Quick capture, unprocessed items
├── 1-Daily/           # Daily notes (YYYY-MM-DD.md)
├── 2-Projects/        # Active projects with deliverables
├── 3-Areas/           # Ongoing responsibilities (no end date)
├── 4-Resources/       # Reference material, topics of interest
├── 5-Archive/         # Completed/inactive items
├── _templates/        # Note templates
├── CLAUDE.md          # AI assistant instructions
├── MEMORY.md          # Long-term memory (decisions, learnings)
└── docs/              # Guides and documentation
    ├── AI-WORKSPACE-GUIDE.md
    ├── AUTOMATION.md
    └── WEEKLY-REVIEW.md
```

## Features

### For Humans
- 📝 Daily note workflow with morning/capture/review sections
- 📁 PARA organization keeps things findable
- 🔗 Wikilinks connect everything
- 📋 Project structure with README/tasks/decisions/ideas
- 🗄️ Clear archival process

### For AI Assistants
- 🤖 `CLAUDE.md` teaches AI your conventions
- 🧠 Autonomous behaviors (smart capture, proactive maintenance)
- 📅 Scheduled automation (morning briefings, inbox processing, reviews)
- 🔄 Session handoff for context continuity

## Getting Started

1. **Fork & Clone** this repository
2. **Open in Obsidian** (File → Open Vault)
3. **Create your first daily note**: `1-Daily/YYYY-MM-DD.md` using the template
4. **Start capturing**: Add thoughts to `0-Inbox/` or directly to your daily note
5. **Set up automation** (optional): See [AUTOMATION.md](docs/AUTOMATION.md)

## Documentation

| Guide | What It Covers |
|-------|----------------|
| [CLAUDE.md](CLAUDE.md) | Vault conventions for AI assistants |
| [AI-WORKSPACE-GUIDE.md](docs/AI-WORKSPACE-GUIDE.md) | Complete setup for AI-assisted development |
| [AUTOMATION.md](docs/AUTOMATION.md) | Setting up cron jobs and scheduled tasks |
| [WEEKLY-REVIEW.md](docs/WEEKLY-REVIEW.md) | Weekly review process and maintenance |

## Customization

### Make It Yours

1. **Edit `CLAUDE.md`** — Adjust conventions to match your style
2. **Modify templates** — Customize `_templates/` for your needs
3. **Add your areas** — Create folders in `3-Areas/` for your responsibilities
4. **Configure automation** — Adjust schedules in [AUTOMATION.md](docs/AUTOMATION.md)

### Opinionated Defaults

This template has opinions. You might disagree. Here's what to change:

| If You Want | Change This |
|-------------|-------------|
| Different folder names | Rename folders + update `CLAUDE.md` references |
| Different daily note format | Edit `_templates/daily.md` |
| No emoji in status | Search/replace in `CLAUDE.md` |
| Flat project structure | Simplify project template, update `CLAUDE.md` |

## Tools Compatibility

Works with:
- **Obsidian** — Primary intended use
- **Claude Code** — Reads CLAUDE.md, supports slash commands
- **OpenCode** — Compatible (uses AGENTS.md alias)
- **Cursor** — Compatible (copy CLAUDE.md to .cursorrules)
- **OpenClaw** — Full automation support with cron jobs
- **Any AI assistant** — CLAUDE.md provides context

## Contributing

Found an improvement? Have a better workflow? PRs welcome!

1. Fork the repo
2. Make your changes
3. Submit a PR with a clear description of the improvement

## License

MIT — Use it, modify it, share it.

---

*Built by humans and AI, for humans and AI.*
