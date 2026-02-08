# Weekly Review Process

A systematic approach to maintaining your vault and synthesizing learnings.

**When:** Sunday evenings (or end of your week)
**Duration:** 30-60 minutes

---

## The Process

### 1. Process Inbox (10 min)

Empty `0-Inbox/` completely:
- [ ] Review each item
- [ ] Route to appropriate location (project, area, resource)
- [ ] Delete or archive anything that's no longer relevant
- [ ] Tag unclear items with `#needs-review` and move to `4-Resources/`

**Goal:** Inbox zero.

### 2. Review Daily Notes (15 min)

Scan through this week's daily notes (`1-Daily/`):
- [ ] What were the key accomplishments?
- [ ] What patterns or themes emerged?
- [ ] Any learnings worth capturing long-term?
- [ ] Any open questions still unresolved?

**Actions:**
- Add significant learnings to project MEMORY sections or a personal MEMORY.md
- Move recurring questions to relevant project's "Open Questions"
- Note anything to carry into next week

### 3. Check Project Health (10 min)

For each active project in `2-Projects/`:
- [ ] Is the status emoji accurate?
  - 🔴 Blocked → Why? What unblocks it?
  - 🟡 In Progress → Is it actually progressing?
  - 🟢 Active → Good to go
- [ ] Is `tasks.md` up to date?
- [ ] Any stale tasks (not touched in 7+ days)?
- [ ] Should this project be archived?

**Red flags:**
- Project not touched in 2+ weeks → Consider archiving or blocking
- Tasks with no progress → Break them down or remove

### 4. Find Orphan Notes (5 min)

Look for notes not linked from anywhere:

```bash
# If using Obsidian with shell access:
# Check for .md files not referenced in any other file
```

Or use Obsidian's Graph View → look for disconnected nodes.

**For each orphan:**
- Link it from an appropriate location, OR
- Move to `4-Resources/` if it's reference material, OR
- Archive to `5-Archive/0-Orphans/`

### 5. Archive Daily Notes (10 min)

Keep `1-Daily/` lean — only recent notes stay live.

**Retention policy:**
- **Keep live:** Current week only (Mon–Sun)
- **Keep live:** Weekly summaries from current month only
- **Keep live:** Monthly summaries (permanent — these are the long-term index)
- **Archive everything older** → `5-Archive/1-Daily/YYYY-MM/`

**Before archiving each note:**
- Extract unfinished tasks → project `tasks.md` or `0-Inbox/`
- Extract key learnings from AI Sync → project notes or MEMORY.md
- Verify the note's week has a weekly summary (create if missing)

**Bloated notes (>100 lines):**
- Move detailed AI Sync session summaries to project `notes/`, leave a link
- Goal: daily notes should be <80 lines after cleanup

**Monthly rollup (first weekly review of a new month):**

When the month turns over, consolidate the previous month's weekly summaries:

1. Read all weekly summaries from the previous month
2. Create `1-Daily/YYYY-MM-monthly.md` with:
   - Combined accomplishments, decisions, learnings
   - Project progress across the month
   - Stats and focus areas for next month
3. Archive the individual weekly summaries to `5-Archive/1-Daily/YYYY-MM/`

**Monthly summary template:**
```markdown
---
type: monthly
created: "YYYY-MM-01"
month: M
year: YYYY
---

# YYYY-MM Monthly Summary

## TL;DR
[2-3 sentence summary of the month]

## Accomplishments
[Consolidated from weekly summaries]

## Projects Progressed
| Project | Status Change | Key Milestones |

## Key Decisions
[Consolidated from weekly summaries]

## Learnings
[Consolidated from weekly summaries]

## Focus for Next Month
[Forward-looking priorities]

## Stats
- Daily notes: N
- Weekly summaries consolidated: N
```

### 6. Archive Other Items (5 min)

**Completed projects:**
- Any projects with ✅ Complete status? Move to `5-Archive/2-Projects/`

**Stale resources:**
- Any resources not accessed in 3+ months? Consider archiving.

### 7. Plan Next Week (5 min)

- [ ] What's the #1 priority for next week?
- [ ] Any deadlines approaching?
- [ ] Any projects needing attention?

Add a "Next Week" section to today's daily note or create Monday's note early.

---

## Weekly Review Checklist

Copy this to your daily note on review day:

```markdown
## 📋 Weekly Review

### Inbox
- [ ] Process all items in 0-Inbox/

### Daily Notes
- [ ] Review this week's dailies
- [ ] Extract key learnings
- [ ] Resolve open questions

### Projects
- [ ] Update status emojis
- [ ] Check for stale tasks
- [ ] Archive completed projects

### Daily Note Archival
- [ ] Archive notes older than current week
- [ ] Extract unfinished tasks before archiving
- [ ] Monthly rollup (if new month)

### Maintenance
- [ ] Find and handle orphan notes
- [ ] Archive completed projects
- [ ] Clean stale resources

### Planning
- [ ] Set #1 priority for next week
- [ ] Note upcoming deadlines
```

---

## Automation

This process can be partially automated with AI assistants.

**With OpenClaw:**
```
# Add to your cron jobs
openclaw cron add --schedule "0 18 * * 0" --text "Run weekly review for vault at /path/to/vault"
```

**With Claude Code:**
```bash
claude
> /project:weekly-review
```

See [AUTOMATION.md](AUTOMATION.md) for full setup.

---

## Tips

1. **Timebox it** — Don't let reviews expand indefinitely. 60 min max.
2. **Be ruthless** — Archive aggressively. You can always un-archive.
3. **Focus on synthesis** — The goal is learning extraction, not just cleanup.
4. **Make it a habit** — Same time every week. Put it on your calendar.

---

## Monthly Deep Clean

Once a month, add these extra steps:

- [ ] Review `4-Resources/` — consolidate similar folders
- [ ] Check folder depth — nothing should be >2 levels in Resources
- [ ] Review archived items — anything to permanently delete?
- [ ] Update `CLAUDE.md` — any conventions to add or change?
