# Evening Sync

End-of-day review and git commit.

## Steps

### 1. Review Today's Daily Note

Open `1-Daily/YYYY-MM-DD.md`:
- [ ] Is "✅ Done Today" section complete?
- [ ] Are all created notes listed in "🔗 Links Created"?

Add to "🤖 AI Sync → AI's Notes":
```markdown
**Evening sync:**
- What we worked on today
- Where we left off
- Suggested next steps
```

### 2. Check Project Consistency

For each project touched today:
- [ ] `tasks.md` — Completed items marked done?
- [ ] `README.md` — Status emoji accurate?
  - 🔴 Blocked
  - 🟡 In Progress
  - 🟢 Ready/Active
  - ✅ Complete
  - 📦 Archived

### 3. Find Orphan Notes

Look for notes created today that aren't linked from anywhere:
- If found, suggest where to link them
- Or add links in today's daily note

### 4. Regenerate CONTEXT.md

- Scan all `2-Projects/*/README.md` files for status and last modified date
- Update the "Active Projects" table with current project states
- List recent daily notes (last 7 days) in "Recent Activity"
- Collect open questions/blockers from project READMEs and recent daily notes
- Write the updated CONTEXT.md to vault root

### 5. Commit to Git

```bash
git add -A
git commit -m "daily: YYYY-MM-DD sync

- [list key changes]
- [mention projects updated]"
git push
```

### 6. Report

Summarize:
- Notes reviewed/updated
- Projects touched
- Orphans found (if any)
- Commit hash (if committed)
