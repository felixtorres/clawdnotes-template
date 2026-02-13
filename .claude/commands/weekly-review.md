# Weekly Review

Deep maintenance — run on Sundays (or your week's end).

**Reference:** See `docs/WEEKLY-REVIEW.md` for full process details.

## Checklist

### 1. Process Inbox (10 min)
- [ ] Review all items in `0-Inbox/`
- [ ] Route each to appropriate location
- [ ] Achieve inbox zero

### 2. Run Full Vault Organization (15 min)
- [ ] Validate frontmatter across all documents
- [ ] Verify locations match document types
- [ ] Check tag taxonomy compliance
- [ ] Audit link health (broken links, orphaned notes)
- [ ] Flag bloated daily notes (>100 lines)
- [ ] Auto-fix safe issues, report complex ones
- [ ] Update `docs/ORGANIZATION_REPORT.md`

### 3. Check for Archival Candidates (5 min)
- [ ] Count daily notes older than current week (Mon-Sun)
- [ ] Check if it's first week of new month (monthly rollup needed)
- [ ] Find completed projects (status: complete, archived)
- [ ] Detect orphaned notes (no wikilinks)

**If archival candidates found:**
- Report counts and suggest running `/project:archive`
- Example: "⚠️ 8 daily notes from January should be archived. Run /project:archive when ready."
- Do NOT archive automatically (user should review first)

### 4. Review Daily Notes (10 min)
- [ ] Scan this week's daily notes
- [ ] Extract key accomplishments
- [ ] Identify patterns or themes
- [ ] Capture significant learnings in MEMORY.md or project notes

### 5. Check Project Health (10 min)

For each project in `2-Projects/`:
- [ ] Is status emoji accurate?
- [ ] Is `tasks.md` up to date?
- [ ] Any stale tasks (7+ days untouched)?
- [ ] Should any projects be archived?

### 6. Plan Next Week (5 min)
- [ ] What's the #1 priority?
- [ ] Any deadlines approaching?
- [ ] Projects needing attention?

## Report

After completing, summarize:
- Items processed from inbox: X
- Organization issues found/fixed: [counts]
- Archival candidates detected: [if any, suggest running /project:archive]
- Learnings captured: [brief list]
- Projects needing attention: [list]
- Next week's top priority: [what]
