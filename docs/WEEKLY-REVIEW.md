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

### 5. Archive Maintenance (5 min)

**Daily notes:**
- If you have 2+ months of daily notes, archive the oldest month
- Move to `5-Archive/1-Daily/YYYY-MM/`

**Completed projects:**
- Any projects with ✅ Complete status? Move to `5-Archive/2-Projects/`

**Stale resources:**
- Any resources not accessed in 3+ months? Consider archiving.

### 6. Plan Next Week (5 min)

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

### Maintenance
- [ ] Find and handle orphan notes
- [ ] Archive old daily notes (if needed)
- [ ] Clean stale resources

### Planning
- [ ] Set #1 priority for next week
- [ ] Note upcoming deadlines
```

---

## Automation

This process can be partially automated with AI assistants.

**With Clawdbot:**
```
# Add to your cron jobs
clawdbot cron add --schedule "0 18 * * 0" --text "Run weekly review for vault at /path/to/vault"
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
