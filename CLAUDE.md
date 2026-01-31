# CLAUDE.md — Agent Instructions

This vault is an Obsidian-based knowledge system. Follow these instructions when working with it.

---

## Vault Structure (PARA)

```
0-Inbox/        → Quick capture, unprocessed items
1-Daily/        → Daily notes (YYYY-MM-DD.md)
2-Projects/     → Active projects with deliverables
3-Areas/        → Ongoing responsibilities (no end date)
4-Resources/    → Reference material, topics of interest
5-Archive/      → Completed/inactive items
_templates/     → Note templates
```

---

## Folder Guidelines

### 2-Projects/
- **One folder per project** — `2-Projects/<project-name>/`
- **Never nest projects** — Each project is a peer
- **Use internal structure** — README, tasks, decisions, ideas, notes/
- **Minimum:** A project must have deliverable(s) and an end state

### 3-Areas/
- **One folder per area** — `3-Areas/<area-name>/`
- **Never nest areas** — Each area is a peer
- **For ongoing work** — No deadline, recurring responsibilities
- Examples: `health/`, `learning/`, `finances/`

### 4-Resources/
⚠️ **Most prone to explosion** — Be disciplined!

**Rules:**
- **Max 2 levels deep** — `4-Resources/<topic>/` or `4-Resources/<topic>/<subtopic>/`
- **Broad categories only** — Aim for 5-10 top-level folders max
- **Use tags over folders** — If tempted to create a subfolder, consider `#tag` instead
- **Archive aggressively** — Move outdated resources to `5-Archive/4-Resources/`

### 0-Inbox/
- **Keep flat** — No subfolders
- **Process regularly** — Items shouldn't live here long

### 1-Daily/
- **Always flat** — No subfolders
- One note per day: `YYYY-MM-DD.md`

### 5-Archive/
- **Mirror the live structure** — `5-Archive/2-Projects/`, etc.
- Move entire folders when archiving

---

## Daily Notes (`1-Daily/YYYY-MM-DD.md`)

Each day has one note. Sections:

- **🌅 Morning** — Tasks planned
- **📝 Capture** — Quick thoughts throughout day
- **💡 Ideas** — Tag with `#idea`, link to projects
- **✅ Done Today** — What was accomplished
- **🔗 Links Created** — Notes created/updated
- **🤖 AI Sync** — Questions for AI + AI's notes

**When working on a day:** Update "Done Today" and "AI Sync" with progress.

---

## Projects (`2-Projects/<name>/`)

Each project has:
- `README.md` — Overview, status, key links
- `tasks.md` — Backlog and current sprint
- `decisions.md` — Decision records (ADRs)
- `ideas.md` — Brainstorming
- `notes/` — Research, design docs, meeting notes

**Status indicators:**
- 🔴 Blocked
- 🟡 In Progress
- 🟢 Ready/Active
- ✅ Complete
- 📦 Archived

**When updating projects:**
1. Update `tasks.md` when items complete
2. Update `README.md` status if phase changes
3. Link new notes in the daily note

---

## Linking Conventions

- Use `[[wikilinks]]` for internal links
- Relative paths: `[[notes/design-doc]]` (within project)
- Absolute paths: `[[2-Projects/project-name/README]]` (cross-project)
- Always update `🔗 Links Created` in daily note when creating notes

---

## Archival Process

### Daily Notes
- **Keep in `1-Daily/`:** Current month + previous month
- **Archive monthly:** Move older notes to `5-Archive/1-Daily/YYYY-MM/`
- **Before archiving:** Ensure key learnings are captured in project notes or MEMORY.md

### Projects
- When complete: Move entire folder to `5-Archive/2-Projects/<name>/`
- Update status to 📦 Archived in README

### Orphan Notes
Notes not linked from anywhere:
1. **Still relevant?** → Link from appropriate location
2. **Reference material?** → Move to `4-Resources/`
3. **No longer needed?** → Move to `5-Archive/0-Orphans/`

---

## Templates

Use templates in `_templates/` for consistency:
- `daily.md` — Daily note structure
- `project-readme.md` — Project overview
- `decision.md` — ADR format

Copy template content when creating new notes of that type.

---

## Autonomous Behaviors

### On Session Start
1. Check if today's daily note exists → create from template if not
2. Read yesterday's daily note for context
3. Note any open questions in "AI Sync" sections

### Smart Capture
When user says "capture: <text>" or drops quick notes:
1. Analyze the content type
2. Route appropriately:
   - **Task** → Add to most relevant project's tasks.md
   - **Idea** → Add to daily note Ideas section with `#idea` tag
   - **Link/reference** → Create in 4-Resources/ with summary
   - **Project concept** → Discuss, then create in 2-Projects/ if confirmed
   - **Unclear** → Add to 0-Inbox/ with `#needs-review`

### Session Handoff
At end of work sessions, update daily note "🤖 AI Sync":
- What we worked on
- Where we left off
- Suggested next steps
- Open questions or blockers

### Proactive Maintenance
While working, if you notice:
- **Duplicate content** → Consolidate and add links
- **Orphan notes** → Suggest where to link them
- **Stale information** → Flag for review
- **Missing links** → Add them

Don't wait for maintenance jobs — fix as you go.

---

## Scheduled Automation

These can run automatically via OpenClaw cron jobs or manually:

| Time | Job | What |
|------|-----|------|
| 8am | Morning Briefing | Create daily note, summarize yesterday |
| Every 6h | Inbox Processing | Triage items in 0-Inbox/ |
| 11pm | Evening Sync | Review, consolidate, commit to GitHub |
| Sunday 6pm | Weekly Review | Deep clean, archive stale, synthesize learnings |

See `docs/AUTOMATION.md` for setup instructions.

---

## Tips for AI Assistants

1. **Don't duplicate** — Link to existing notes rather than repeating content
2. **Be concise** — Notes should be scannable, not walls of text
3. **Use frontmatter** — YAML frontmatter for structured metadata when useful
4. **Progressive detail** — Overview first, details in linked notes
5. **Date everything** — Include dates in notes that capture point-in-time info
