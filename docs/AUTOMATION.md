# Automation Guide

Set up scheduled tasks to maintain your vault automatically.

---

## Overview

| Time | Job | What It Does |
|------|-----|--------------|
| 8am daily | Morning Briefing | Creates daily note, summarizes yesterday |
| Every 6h | Inbox Processing | Triages items in 0-Inbox/ |
| 11pm daily | Evening Sync | Reviews day, commits to GitHub |
| Sunday 6pm | Weekly Review | Deep clean, archive, synthesize |

---

## Option 1: OpenClaw (Recommended)

[OpenClaw](https://github.com/openclaw/openclaw) is an AI assistant with built-in cron job support.

### Setup

1. **Install OpenClaw:**
   ```bash
   npm install -g openclaw
   openclaw init
   ```

2. **Add cron jobs:**
   ```bash
   # Morning briefing at 8am
   openclaw cron add --schedule "0 8 * * *" --text "Morning briefing for vault at /path/to/your/vault.

   Read CLAUDE.md for conventions, then:
   1. Create today's daily note if it doesn't exist
   2. Summarize yesterday's daily note
   3. Check active project status
   4. Send brief summary (10 lines max)"

   # Inbox processing every 6 hours
   openclaw cron add --schedule "0 */6 * * *" --text "Process inbox for vault at /path/to/your/vault.

   For each item in 0-Inbox/:
   1. Analyze content type
   2. Route to appropriate location
   3. Report what was processed"

   # Evening sync at 11pm
   openclaw cron add --schedule "0 23 * * *" --text "Evening sync for vault at /path/to/your/vault.

   1. Review today's daily note
   2. Ensure Done Today is complete
   3. Check for orphan notes created today
   4. Commit and push to GitHub"

   # Weekly review Sunday 6pm
   openclaw cron add --schedule "0 18 * * 0" --text "Weekly review for vault at /path/to/your/vault.

   Follow the process in docs/WEEKLY-REVIEW.md:
   1. Process inbox to zero
   2. Review this week's daily notes
   3. Check project health
   4. Find and handle orphans
   5. Archive old items
   6. Send summary of what was cleaned"
   ```

3. **Start the gateway:**
   ```bash
   openclaw gateway start
   ```

### Managing Jobs

```bash
# List all jobs
openclaw cron list

# Run a job manually
openclaw cron run <job-id>

# Remove a job
openclaw cron remove <job-id>
```

---

## Option 2: Claude Code Slash Commands

If using Claude Code without OpenClaw, create manual slash commands.

### Setup

Create `.claude/commands/` in your vault:

```bash
mkdir -p .claude/commands
```

### Morning Briefing

**File:** `.claude/commands/morning-briefing.md`

```markdown
# Morning Briefing

Start the day with context.

## Steps

1. **Check today's daily note:**
   - If `1-Daily/YYYY-MM-DD.md` doesn't exist, create it from `_templates/daily.md`
   - Replace {{date:YYYY-MM-DD}} with today's date
   - Replace {{date:dddd}} with day name

2. **Read yesterday's daily note:**
   - Extract key accomplishments from "Done Today"
   - Note any open questions from "AI Sync"

3. **Check active projects:**
   - List projects with status 🟡 or 🟢
   - Flag any with tasks not updated in 7+ days

4. **Summarize:**
   - Yesterday's highlights (2-3 bullets)
   - Active projects needing attention
   - Suggested focus for today

Keep it concise — 10 lines max.
```

### Inbox Processing

**File:** `.claude/commands/inbox.md`

```markdown
# Process Inbox

Triage items in 0-Inbox/.

## For Each Item

1. **Analyze content type:**
   - Task? → Route to relevant project's tasks.md
   - Idea? → Add to daily note Ideas with #idea tag
   - Reference? → Create note in 4-Resources/
   - Project concept? → Create in 2-Projects/ with template
   - Unclear? → Add #needs-review tag, move to 4-Resources/

2. **After processing:**
   - Delete the original inbox item
   - Update daily note Links Created section

## Report

List what was processed and where it went.
```

### Evening Sync

**File:** `.claude/commands/sync.md`

```markdown
# Evening Sync

End-of-day review and git commit.

## Steps

1. **Review today's daily note:**
   - Is "Done Today" complete?
   - Add to "AI's Notes" with session summary

2. **Check consistency:**
   - For each project touched today:
     - [ ] tasks.md updated?
     - [ ] README.md status accurate?

3. **Find today's orphans:**
   - Any new notes not linked from anywhere?
   - Suggest where to link them

4. **Commit to git:**
   ```bash
   git add -A
   git commit -m "daily: YYYY-MM-DD sync

   - [list what changed]"
   git push
   ```

Report what was committed.
```

### Weekly Review

**File:** `.claude/commands/weekly-review.md`

```markdown
# Weekly Review

Deep maintenance — run on Sundays.

Follow the full process in docs/WEEKLY-REVIEW.md.

## Checklist

- [ ] Inbox → zero
- [ ] Daily notes reviewed, learnings extracted
- [ ] Project statuses accurate
- [ ] Stale tasks flagged
- [ ] Orphan notes handled
- [ ] Old daily notes archived
- [ ] Completed projects archived

## Report

Summarize:
- Items processed from inbox
- Learnings captured
- Projects needing attention
- Items archived
- Next week's priority
```

### Usage

```bash
cd /path/to/vault
claude
> /project:morning-briefing
> /project:inbox
> /project:sync
> /project:weekly-review
```

---

## Option 3: System Cron + Script

For non-AI automation (basic file operations only).

### Archive Old Daily Notes

**File:** `scripts/archive-daily-notes.sh`

```bash
#!/bin/bash
# Archives daily notes older than 60 days

VAULT_PATH="$1"
DAILY_DIR="$VAULT_PATH/1-Daily"
ARCHIVE_DIR="$VAULT_PATH/5-Archive/1-Daily"

# Find notes older than 60 days
find "$DAILY_DIR" -name "*.md" -mtime +60 | while read file; do
    # Extract YYYY-MM from filename
    filename=$(basename "$file")
    month=$(echo "$filename" | cut -d'-' -f1-2)
    
    # Create archive directory
    mkdir -p "$ARCHIVE_DIR/$month"
    
    # Move file
    mv "$file" "$ARCHIVE_DIR/$month/"
    echo "Archived: $filename → $month/"
done
```

**Cron entry:**
```bash
# Run monthly on the 1st at 2am
0 2 1 * * /path/to/scripts/archive-daily-notes.sh /path/to/vault
```

---

## Git Auto-Commit

For automatic daily backups without AI.

**File:** `scripts/auto-commit.sh`

```bash
#!/bin/bash
VAULT_PATH="$1"
cd "$VAULT_PATH"

# Check if there are changes
if [[ -n $(git status -s) ]]; then
    git add -A
    git commit -m "auto: $(date +%Y-%m-%d) backup"
    git push
    echo "Committed changes"
else
    echo "No changes to commit"
fi
```

**Cron entry:**
```bash
# Run nightly at 11:30pm
30 23 * * * /path/to/scripts/auto-commit.sh /path/to/vault
```

---

## Troubleshooting

### Cron jobs not running

1. Check cron is enabled: `systemctl status cron`
2. Check job list: `openclaw cron list` or `crontab -l`
3. Check logs: `openclaw gateway logs` or `/var/log/syslog`

### AI not finding vault

- Use absolute paths in cron job text
- Verify CLAUDE.md exists in vault root
- Check AI has read access to the directory

### Git push failing

- Ensure SSH keys are configured
- Check remote is set: `git remote -v`
- Verify authentication: `ssh -T git@github.com`
