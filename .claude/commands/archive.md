# Archive Old Content

Automated archival of old daily notes, completed projects, and orphaned content following CONVENTIONS.md rules.

**Safety:** Always shows what will be archived before moving files. Runs in dry-run mode first.

Read CLAUDE.md and docs/CONVENTIONS.md before running.

---

## What Gets Archived

### 1. Daily Notes (Weekly Cleanup)
- **Keep:** Current week only (Monday-Sunday)
- **Archive:** Older daily notes → `5-Archive/1-Daily/YYYY-MM/`
- **Keep:** Weekly summaries from current month
- **Archive:** Previous months' weekly summaries (after rollup)

### 2. Monthly Rollup (Monthly Task)
- **When:** First week of new month
- **Action:** Consolidate previous month's weekly summaries into `YYYY-MM-monthly.md`
- **Then:** Archive individual weekly files to `5-Archive/1-Daily/YYYY-MM/`
- **Keep:** Monthly summary in `1-Daily/` permanently

### 3. Completed Projects
- **Find:** Projects with `status: complete` or `status: archived`
- **Archive:** Move entire folder to `5-Archive/2-Projects/<name>/`
- **Update:** README status to 📦 Archived

### 4. Orphaned Notes
- **Find:** Notes with no incoming or outgoing wikilinks
- **Exclude:** README, CONTEXT, templates, daily notes, tasks/ideas files
- **Archive:** Move to `5-Archive/0-Orphans/YYYY-MM/`

---

## Steps

### Phase 1: Discovery & Preview (Dry-Run)

**1. Scan for archival candidates:**

```python
# Daily notes
current_week = get_current_week()  # Mon-Sun
old_dailies = [d for d in daily_notes if d not in current_week]

# Monthly rollup check
if is_first_week_of_month():
    last_month_weeklies = get_last_month_weekly_summaries()

# Completed projects
completed_projects = [p for p in projects if p.status in ['complete', 'archived']]

# Orphaned notes
orphans = find_notes_with_no_links(exclude_system_files=True)
```

**2. Generate preview report:**

```markdown
# Archive Preview (Dry-Run)

## Daily Notes (8 files)
Moving to 5-Archive/1-Daily/2026-01/:
- 2026-01-27.md
- 2026-01-28.md
- 2026-01-29.md
- 2026-01-30.md
- 2026-01-31.md
- 2026-02-01.md
- 2026-02-02.md
- 2026-02-03.md

## Monthly Rollup (February detected)
Creating: 1-Daily/2026-01-monthly.md
Consolidating from:
- 2026-W04-weekly.md
- 2026-W05-weekly.md

## Completed Projects (0 files)
None detected.

## Orphaned Notes (2 files)
Moving to 5-Archive/0-Orphans/2026-02/:
- 4-Resources/old-article.md (no links)
- 2-Projects/misc-note.md (no links)

────────────────────────────────────────
Total: 10 files to archive
Proceed? (y/N)
```

**3. Ask for confirmation**

If user approves, proceed to Phase 2. Otherwise, exit.

---

### Phase 2: Pre-Archive Checks

**Before moving files, verify:**

1. **Extract unfinished tasks:**
   - Scan daily notes for unchecked `- [ ]` items
   - Move to appropriate project `tasks.md` or `0-Inbox/`
   - Report what was extracted

2. **Verify bloated notes trimmed:**
   - Daily notes >100 lines should have detailed content moved to project notes first
   - Warn if bloated notes detected
   - Suggest running cleanup before archiving

3. **Check for unprocessed inbox:**
   - If `0-Inbox/` has items, warn
   - Suggest processing inbox first

4. **Verify wikilinks won't break:**
   - Check if files being archived are linked from active notes
   - Update links to archived paths (e.g., `[[2026-01-27]]` → `[[5-Archive/1-Daily/2026-01/2026-01-27]]`)

---

### Phase 3: Archive Execution

**1. Create archive directories:**

```bash
mkdir -p 5-Archive/1-Daily/2026-01
mkdir -p 5-Archive/1-Daily/2026-02
mkdir -p 5-Archive/2-Projects
mkdir -p 5-Archive/0-Orphans/2026-02
```

**2. Archive daily notes:**

```bash
# Move old dailies
for file in old_daily_notes:
    month = extract_month(file)  # 2026-01
    mv "1-Daily/${file}" "5-Archive/1-Daily/${month}/"
    echo "✓ Archived ${file}"
```

**3. Monthly rollup (if applicable):**

```bash
# Create monthly summary
cat > 1-Daily/2026-01-monthly.md <<EOF
---
type: monthly
created: "2026-01-27"
month: 1
year: 2026
---

# January 2026 Monthly Summary

## Week 4 (Jan 20-26)
[Content from 2026-W04-weekly.md]

## Week 5 (Jan 27-Feb 2)
[Content from 2026-W05-weekly.md]

## Key Accomplishments
- [Extracted highlights]

## Projects Advanced
- [Project progress]

## Decisions Made
- [Key decisions]

## Learnings
- [Insights gained]
EOF

# Archive weekly summaries
mv "1-Daily/2026-W04-weekly.md" "5-Archive/1-Daily/2026-01/"
mv "1-Daily/2026-W05-weekly.md" "5-Archive/1-Daily/2026-01/"
```

**4. Archive completed projects:**

```bash
for project in completed_projects:
    # Update status if not already archived
    if status != 'archived':
        update_frontmatter(status='archived')
        update_readme_emoji('📦 Archived')

    # Move entire folder
    mv "2-Projects/${project}" "5-Archive/2-Projects/"
    echo "✓ Archived project: ${project}"
```

**5. Archive orphaned notes:**

```bash
for orphan in orphaned_notes:
    mv "${orphan}" "5-Archive/0-Orphans/2026-02/"
    echo "✓ Archived orphan: ${orphan}"
```

---

### Phase 4: Update References

**1. Fix broken wikilinks:**

For each file that was archived, update links in active notes:
```
[[2026-01-27]] → [[5-Archive/1-Daily/2026-01/2026-01-27]]
[[old-project/README]] → [[5-Archive/2-Projects/old-project/README]]
```

**2. Update CONTEXT.md:**

If CONTEXT.md references archived content, update paths.

**3. Verify no broken links:**

Run link health check on remaining active notes.

---

### Phase 5: Commit & Report

**1. Git commit:**

```bash
git add -A
git commit -m "archive: $(date +%Y-%m-%d) cleanup

- Daily notes: X files archived to 5-Archive/1-Daily/
- Monthly rollup: YYYY-MM-monthly.md created
- Projects: Y projects archived
- Orphans: Z notes archived

Extracted tasks: N moved to inbox/projects
Updated links: M references fixed"
git push
```

**2. Generate report:**

```markdown
# Archive Report

## Daily Notes
✓ Archived 8 daily notes to 5-Archive/1-Daily/2026-01/
✓ Current week (Feb 10-16) kept in 1-Daily/

## Monthly Rollup
✓ Created 2026-01-monthly.md (consolidated 2 weekly summaries)
✓ Archived weekly summaries to 5-Archive/1-Daily/2026-01/

## Projects
✓ No completed projects to archive

## Orphans
✓ Archived 2 orphaned notes to 5-Archive/0-Orphans/2026-02/

## Cleanup
✓ Extracted 3 unfinished tasks to inbox
✓ Updated 5 wikilink references
✓ No broken links detected

────────────────────────────────────────
Total archived: 10 files
Vault is clean for current week ✨
```

---

## Safety Features

### 1. Dry-Run First
Always preview before executing. Show exactly what will move.

### 2. Task Extraction
Never archive unfinished tasks - extract them first.

### 3. Link Preservation
Update all references to archived files automatically.

### 4. Bloat Warning
Detect bloated notes and suggest cleanup before archiving.

### 5. Rollback Info
Report includes git commit hash for easy rollback if needed.

---

## Usage Patterns

### Weekly (Recommended)
```
# Part of weekly review routine
/project:weekly-review  # Detects old items
/project:archive        # Archives them
```

### Monthly (First Week)
```
# Creates monthly summary
/project:archive  # Consolidates previous month's weeklies
```

### Ad-Hoc
```
# Anytime vault feels cluttered
/project:archive  # Clean up old content
```

---

## What NOT to Archive

**Never archive:**
- Current week's daily notes (Mon-Sun)
- Current month's weekly summaries
- Active projects (status: active, proposed, accepted)
- Monthly summaries (keep permanently)
- System files (README, CONTEXT, CLAUDE)
- Templates
- Documentation (docs/ folder)

**Manual review needed:**
- Projects with status: complete but recent activity
- Notes with links from active content
- Files modified in last 7 days (even if old)

---

## Output

Report to user:
1. What was archived (counts + paths)
2. Any tasks extracted
3. Links updated
4. Warnings/issues encountered
5. Git commit hash
6. Current vault state (dailies count, active projects)

**Example:**
```
✨ Archive complete!

📁 Archived:
   - 8 daily notes (Jan 27 - Feb 3)
   - 2 weekly summaries → monthly rollup
   - 2 orphaned notes

📋 Extracted:
   - 3 unfinished tasks → 0-Inbox/

🔗 Updated:
   - 5 wikilink references

📊 Current State:
   - Daily notes: 7 (current week)
   - Active projects: 2
   - Vault clean ✓

Git: bd1c9ac
```
