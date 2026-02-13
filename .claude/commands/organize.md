# Document Review & Organization

Comprehensive vault maintenance: validate frontmatter, verify locations, check tag taxonomy, and audit link health.

Read CLAUDE.md and docs/CONVENTIONS.md before running.

## Steps

### 1. Frontmatter Validation

Scan all markdown files (excluding templates, CONTEXT.md) and check:

- **Required fields by type:**
  - `daily`: `type`, `created`
  - `project`: `type`, `status`, `created`
  - `decision`: `type`, `status`, `created`, `project`
  - `tasks`: `type`, `project`
  - `ideas`: `type`, `project`
  - `resource`: `type`, `created`, `updated`
  - `prd`: `type`, `status`, `created`, `project`
  - `dev-plan`: `type`, `status`, `created`, `project`, `prd`

- **Valid status values:** `active`, `proposed`, `accepted`, `complete`, `archived`, `deprecated`

**Auto-fix:**
- Missing `created` → Add today's date
- Missing `updated` on resources → Add today's date
- Invalid status values → Flag for manual review

**Report:** Files missing required fields, invalid values

---

### 2. Location Verification

Check that documents are in the correct folders based on their type:

| Type | Expected Location | Notes |
|------|------------------|-------|
| `daily` | `1-Daily/` | Must match `YYYY-MM-DD.md` or `YYYY-Www-weekly.md` format |
| `project` | `2-Projects/<name>/README.md` | Root README only |
| `tasks` | `2-Projects/<name>/tasks.md` | Or `3-Areas/<name>/tasks.md` |
| `ideas` | `2-Projects/<name>/ideas.md` | Or `3-Areas/<name>/ideas.md` |
| `decision` | `2-Projects/<name>/decisions.md` or `notes/` | |
| `prd` | `2-Projects/<name>/features/<feature>/PRD.md` | Feature-specific |
| `dev-plan` | `2-Projects/<name>/features/<feature>/DEV_PLAN.md` | Matches PRD |
| `resource` | `4-Resources/` | Reference material |

**Auto-fix:**
- Daily notes in wrong location → Report only (manual move required)
- Resources in wrong folder → Suggest correct location

**Report:** Misplaced files with suggested target locations

---

### 3. Tag Taxonomy Check

Validate all frontmatter `tags: []` follow the taxonomy:

**Domain tags:** `ai`, `web`, `python`, `design`, `devops`
**Type tags:** `idea`, `decision`, `research`, `tutorial`, `reference`
**Status tags:** `active`, `stale`, `blocked`

**Checks:**
- No more than 15 tags per document (flag excessive tagging)
- Tags are lowercase and hyphen-separated
- Inline hashtags like `#idea` in daily notes are fine (skip validation)

**Auto-fix:**
- Remove duplicate tags
- Convert `camelCase` or `snake_case` to `kebab-case`
- Flag unknown tags (not in taxonomy) for review

**Report:** Files with invalid tags, excessive tags, suggestions for cleanup

---

### 4. Link Health Audit

Scan for:

1. **Broken wikilinks:** `[[target]]` where target doesn't exist
2. **Orphaned notes:** Files with no incoming or outgoing links
3. **Missing backlinks:** Related documents that should reference each other

**Auto-fix:**
- Nothing (links require manual review)

**Report:**
- List of broken links with source file location
- Orphaned notes (exclude templates, CONTEXT.md, README.md)
- Suggestions for connecting related documents

---

### 5. Bloat Detection

Flag daily notes over 100 lines:
- Suggest moving detailed "AI Sync" sections to project `notes/` folder
- Leave summary + link in daily note

**Auto-fix:** None (manual review required)

**Report:** Bloated daily notes with line counts

---

### 6. Generate Organization Report

Create or update `docs/ORGANIZATION_REPORT.md` with:

```markdown
# Vault Organization Report
Generated: YYYY-MM-DD

## Summary
- Total files scanned: X
- Issues auto-fixed: Y
- Issues flagged for review: Z

## Frontmatter Issues
[List files with missing/invalid frontmatter]

## Location Issues
[List misplaced files with suggestions]

## Tag Issues
[List tag violations and suggestions]

## Link Health
- Broken links: X
- Orphaned notes: Y
[Detailed list]

## Bloated Notes
[List daily notes >100 lines]

## Recommendations
[Prioritized list of cleanup actions]
```

---

### 7. Commit Changes

If auto-fixes were made:

```bash
git add -A
git commit -m "organize: vault maintenance $(date +%Y-%m-%d)

- Frontmatter: X files fixed
- Tags: Y duplicates removed
- Report: docs/ORGANIZATION_REPORT.md updated"
git push
```

---

## Output

Report:
1. Number of files scanned
2. Auto-fixes applied (with details)
3. Issues flagged for manual review
4. Link to full report: `docs/ORGANIZATION_REPORT.md`
5. Suggested next actions prioritized by impact
