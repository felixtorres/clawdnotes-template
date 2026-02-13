# Vault Conventions

Detailed rules for folder organization, commit formatting, pre-commit workflow, and archival.

---

## Folder Organization Guidelines

### When to Create New Folders

#### 2-Projects/
- **One folder per project** — `2-Projects/<project-name>/`
- **Never nest projects** — Each project is a peer
- **Use internal structure** — README, tasks, decisions, ideas, notes/
- **Minimum:** A project must have deliverable(s) and an end state

#### 3-Areas/
- **One folder per area** — `3-Areas/<area-name>/`
- **Never nest areas** — Each area is a peer
- **For ongoing work** — No deadline, recurring responsibilities
- Examples: `health/`, `learning/`, `finances/`

#### 4-Resources/
⚠️ **Most prone to explosion** — Be disciplined!

**Gate:** Before placing anything here, confirm it passes ALL three:
1. It's not actionable (not a task, not part of a project)
2. It doesn't belong to an ongoing area of responsibility
3. You expect to reference it again in the future

If it fails any check, it belongs somewhere else (project, area, or archive).

**Rules:**
- **Never place here during capture** — Items arrive here only via inbox triage
- **Max 2 levels deep** — `4-Resources/<topic>/` or `4-Resources/<topic>/<subtopic>/`
- **Broad categories only** — Aim for 5-10 top-level folders max
- **Use tags over folders** — If tempted to create a subfolder, consider `tags: [...]` in frontmatter instead
- **Archive aggressively** — Move outdated resources to `5-Archive/4-Resources/`

**Examples of good top-level folders:**
```
4-Resources/
  ai/              → AI, ML, LLMs, prompting
  dev/             → Programming, tools, workflows
  business/        → Finance, productivity, frameworks
  health/          → Fitness, nutrition, mental health
  design/          → UI, UX, visual design
```

**When to create a subfolder:**
- Only if you have 10+ notes on a specific subtopic

#### 0-Inbox/
- **Keep flat** — No subfolders
- **Default landing zone** — When in doubt, capture here first
- **Process regularly** — Items shouldn't live here longer than one triage cycle
- **Triage destination checklist:** For each item, ask in order:
  1. Does it belong to an active project? → Move to project
  2. Does it belong to an area? → Move to area
  3. Is it reference material I'll look up again? → Move to `4-Resources/`
  4. Is it a one-off note? → Link from daily note, then archive

#### 1-Daily/
- **Always flat** — No subfolders
- One note per day: `YYYY-MM-DD.md`

#### 5-Archive/
- **Mirror the live structure** — `5-Archive/2-Projects/`, etc.
- Move entire folders when archiving

### Project Internal Structure

Projects grow in complexity over time. Structure them based on size:

#### Small Projects (1-5 files)
**Structure:**
```
2-Projects/<name>/
├── README.md      ← Overview, status, key links
├── tasks.md       ← Task list
├── ideas.md       ← Brainstorming
└── PRD.md         ← Product requirements (if applicable)
```
**No subfolders needed.** Keep everything at root level.

---

#### Medium Projects (5-15 files)
**Add `features/` folder for multi-feature projects:**
```
2-Projects/<name>/
├── README.md
├── tasks.md
├── ideas.md
├── decisions.md
├── PRD.md              ← Overall project PRD
└── features/
    ├── feature-a/
    │   ├── PRD.md
    │   └── DEV_PLAN.md
    └── feature-b/
        └── PRD.md
```
**When to use:** When project has 3+ distinct features that need isolated planning/development.

---

#### Large Projects (15+ files)
**Add topic-based subfolders:**
```
2-Projects/<name>/
├── README.md
├── tasks.md
├── ideas.md
├── decisions.md
├── PRD.md
├── features/           ← Feature PRDs & DEV_PLANs
│   ├── feature-a/
│   │   ├── PRD.md
│   │   └── DEV_PLAN.md
│   └── feature-b/
├── design/             ← Architecture & design docs
│   ├── architecture.md
│   ├── data-model.md
│   └── ui-design.md
├── research/           ← Research & evaluation
│   ├── research-tech-x.md
│   └── research-alternatives.md
└── comparisons/        ← Market/competitive analysis (optional)
    └── competitor-analysis.md
```

**Folder purposes:**
- **`features/`** — Feature-specific PRDs, DEV_PLANs, and implementation notes
- **`design/`** — Architecture decisions, system design, data models, UI/UX design
- **`research/`** — Technology evaluation, experiments, proofs-of-concept
- **`comparisons/`** — Market analysis, competitor research, product comparisons

**Naming conventions:**
- Design docs: `architecture.md`, `data-model.md`, `ui-design.md`
- Research: `research-<topic>.md` (e.g., `research-neo4j-vs-kuzu.md`)
- Features: `<feature-name>/PRD.md` and `<feature-name>/DEV_PLAN.md`

**When to create subfolders:**
- Wait until you have **5+ files** of a specific type
- Create `design/` when you have multiple architecture/design docs
- Create `research/` when evaluating multiple technologies/approaches
- Create `comparisons/` if doing competitive analysis

**Migration from `notes/`:**
If you have an existing `notes/` folder, migrate to structured folders:
1. **Design/architecture** → `design/`
2. **Research/evaluation** → `research/`
3. **Competitive analysis** → `comparisons/`
4. **Feature-specific** → `features/<name>/`

---

### Project-Specific vs General Resources

**Key principle:** Link, don't duplicate.

| Content Type | Location | Example |
|--------------|----------|---------|
| **Project-specific research** | `2-Projects/<name>/research/` | Evaluating database X for project Y |
| **General reference material** | `4-Resources/` | How databases work (general) |
| **Project using general concept** | Link from project to resource | `[[4-Resources/tech/database-patterns]]` |
| **Application notes** | `2-Projects/<name>/design/` or root | "How we apply pattern X" |

**Decision tree:**
1. **Is this research for a specific active project?** → `2-Projects/<name>/research/`
2. **Will this be useful across multiple projects?** → `4-Resources/`
3. **Not sure yet?** → Start in `0-Inbox/`, process during triage

---

### Folder Creation Checklist

Before creating a new folder, ask:
1. Can this use an existing category?
2. Will this have 5+ notes? (Otherwise, just use tags)
3. Is this a permanent category? (Or temporary interest?)
4. Can tags solve this instead? (Usually yes for Resources)

### Periodic Cleanup (Weekly Review)

- [ ] Consolidate similar resource folders
- [ ] Archive stale resources
- [ ] Check for folders with <3 notes → flatten or remove
- [ ] Verify no folders are >2 levels deep (except project internals)

---

## Commit Message Format

```
<type>: <short summary>

- Detail 1
- Detail 2
```

**Types:**
- `daily` — Regular daily sync
- `project` — Project-specific updates
- `design` — Design documents
- `research` — Research notes
- `archive` — Moving items to archive
- `fix` — Corrections or consolidations

**Examples:**
```
daily: 2026-01-28 sync

- db-insight-graph: Completed design phase
- Created PRD for developer handoff

project: db-insight-graph design complete

- Pattern Library design
- PRD ready for implementation
```

---

## Pre-Commit Workflow

Before committing:

1. **Review today's daily note** — Ensure "Done Today" is current, "AI Sync" has session summary, "Links Created" is complete
2. **Check project consistency** — For each project touched: `tasks.md` items marked, `README.md` status emoji accurate
3. **Consolidate redundancy** — Duplicate info → single source. Outdated info → update/archive. Orphan notes → link/archive
4. **Commit and push** with descriptive message

---

## Archival Process

### Daily Notes
- **Keep in `1-Daily/`:** Current week only (Mon–Sun)
- **Keep weekly summaries:** Only from current month; older ones get rolled up
- **Archive during weekly review:** Move older notes to `5-Archive/1-Daily/YYYY-MM/`
- **Monthly rollup:** On first weekly review of a new month, consolidate previous month's weekly summaries into `YYYY-MM-monthly.md`, then archive the weeklies
- **Before archiving:**
  - Extract unfinished tasks → project `tasks.md` or `0-Inbox/`
  - Ensure key learnings captured in project notes or MEMORY.md
  - For bloated notes (>100 lines): move detailed AI Sync content to project `notes/`, leave a link
- **Goal:** `1-Daily/` should have ~10 files max (dailies + current month weeklies + monthly summaries)

### Projects
- When complete: Move entire folder to `5-Archive/2-Projects/<name>/`
- Update status to 📦 Archived in README

### Orphan Notes
1. **Still relevant?** → Link from appropriate location
2. **Reference material?** → Move to `4-Resources/`
3. **No longer needed?** → Move to `5-Archive/0-Orphans/`

---

## Status Indicators

Use these emoji consistently in project READMEs:
- 🔴 Blocked
- 🟡 In Progress
- 🟢 Ready/Active
- ✅ Complete
- 📦 Archived
