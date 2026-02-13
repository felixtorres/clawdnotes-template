# CLAUDE.md — Agent Instructions

This vault is an Obsidian-based knowledge system (PARA-inspired). Follow these instructions.

See `docs/CONVENTIONS.md` for detailed folder rules, commit format, and archival process.
See `CONTEXT.md` for current vault state (auto-updated by /sync).

---

## Vault Structure

```
0-Inbox/        → Quick capture, unprocessed items
1-Daily/        → Daily notes (YYYY-MM-DD.md)
2-Projects/     → Active projects with deliverables
3-Areas/        → Ongoing responsibilities (no end date)
4-Resources/    → Reference material, topics of interest
5-Archive/      → Completed/inactive items
_templates/     → Note templates
MEMORY.md       → Long-term memory (decisions, learnings, preferences)
CONTEXT.md      → Vault state index (auto-generated)
```

---

## Frontmatter Schema

Every note MUST have YAML frontmatter. The `type` field is required.

| Type | Required Fields | Optional Fields |
|------|----------------|-----------------|
| `daily` | `type`, `created` | |
| `project` | `type`, `status`, `created` | `target`, `tags` |
| `decision` | `type`, `status`, `created`, `project` | `tags` |
| `tasks` | `type`, `project` | |
| `ideas` | `type`, `project` | |
| `resource` | `type`, `created`, `updated` | `tags`, `related` |
| `prd` | `type`, `status`, `created`, `project` | `tags` |
| `dev-plan` | `type`, `status`, `created`, `project`, `prd` | `tags` |

**`status` values:** `active`, `proposed`, `accepted`, `complete`, `archived`, `deprecated`
**`related`:** Optional field for explicit cross-linking: `related: [note-a, note-b]`

---

## Tag Taxonomy

Use frontmatter `tags: []` for canonical tags. Keep to ~15 tags max.

**Domain:** `ai`, `web`, `python`, `design`, `devops`
**Type:** `idea`, `decision`, `research`, `tutorial`, `reference`
**Status:** `active`, `stale`, `blocked`

Inline `#idea` in daily notes is fine as quick-capture shorthand.

---

## Note Structure Rules

- Any note over 50 lines should start with a `## TL;DR` section (2-3 sentences)
- Use `[[wikilinks]]` for internal links
- Relative paths within project: `[[notes/design-doc]]`
- Absolute paths cross-project: `[[2-Projects/project-name/README]]`
- Always update `🔗 Links Created` in daily note when creating notes

---

## Projects (`2-Projects/<name>/`)

Each project has: `README.md`, `tasks.md`, `decisions.md`, `ideas.md`, `notes/`

When updating:
1. Update `tasks.md` when items complete
2. Update `README.md` status if phase changes
3. Link new notes in the daily note

---

## Feature Development Workflow

For significant features, follow the structured workflow. See `docs/FEATURE-WORKFLOW.md` for full details.

**Folder structure:**
```
2-Projects/<project>/features/<feature-name>/
├── PRD.md          # What & why (required)
├── DEV_PLAN.md     # How (after PRD approved)
└── decisions.md    # Feature-specific ADRs (optional)
```

**When to use:**
- New feature that needs design thinking → Start with PRD
- Small fix/tweak → Skip, just do it
- Prototype/spike → Lightweight PRD with `status: spike`

**Workflow:**
1. **Idea** → Add to `ideas.md`
2. **PRD** → Create `features/<name>/PRD.md` using `[[_templates/feature-prd]]`
3. **DEV_PLAN** → Create `features/<name>/DEV_PLAN.md` using `[[_templates/dev-plan]]`
4. **Implement** → Work through phases, update tasks.md

**When user says "new feature: <name>":**
1. Create `features/<name>/` folder in the relevant project
2. Create PRD.md from template
3. Help fill in problem statement and requirements

---

## Autonomous Behaviors

### On Session Start
1. Check if today's daily note exists → create from template if not
2. Read yesterday's daily note for context
3. Note any open questions in "AI Sync" sections

### Smart Capture
When user says "capture: <text>", route using this priority order (first match wins):

1. **Belongs to an active project?** → Add to that project's `tasks.md`, `ideas.md`, or `notes/`
2. **Belongs to an active area?** → Add to that area's folder in `3-Areas/`
3. **Task with no clear project** → Add to `0-Inbox/` with `#task`
4. **Idea** → Add to daily note Ideas section with `#idea`
5. **Project concept** → Discuss, then create in `2-Projects/` if confirmed
6. **Everything else** → Add to `0-Inbox/`

**Inbox is the default.** Only create in `4-Resources/` during inbox processing (not during capture) when an item is confirmed reference material that doesn't belong to any project or area.

**Never skip the Inbox for references.** Links, articles, and notes that aren't clearly tied to a project/area go to `0-Inbox/` first — they get triaged to `4-Resources/` later during inbox processing.

### Session Handoff
At end of work sessions, update daily note "🤖 AI Sync":
- What we worked on, where we left off
- Suggested next steps, open questions

### Proactive Maintenance
While working, fix as you go:
- **Duplicate content** → Consolidate and add links
- **Orphan notes** → Suggest where to link them
- **Stale information** → Flag for review
- **Missing links** → Add them

---

## Scheduled Automation

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
3. **Use frontmatter** — Every note gets YAML frontmatter
4. **Progressive detail** — Overview first, details in linked notes
5. **Date everything** — Include dates in notes that capture point-in-time info
