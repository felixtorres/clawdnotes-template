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

> **Design principle:** Cron payloads reference the slash command files (`.claude/commands/*.md`)
> rather than duplicating the workflow inline. This way, updating a slash command automatically
> updates the cron job behavior — single source of truth.

### Setup

1. **Install OpenClaw:**
   ```bash
   npm install -g openclaw
   openclaw init
   ```

2. **Add cron jobs:**
   ```bash
   VAULT=/path/to/your/vault

   # Morning briefing at 8am
   openclaw cron add --schedule "0 8 * * *" --text \
     "Run the morning briefing for the vault at $VAULT. Read CLAUDE.md for conventions, then read and execute the workflow in .claude/commands/morning-briefing.md. Follow every step exactly as documented."

   # Inbox processing every 6 hours
   openclaw cron add --schedule "0 */6 * * *" --text \
     "Process the inbox for the vault at $VAULT. Read CLAUDE.md for conventions, then read and execute the workflow in .claude/commands/inbox.md. Follow every step exactly. If inbox is empty, reply: HEARTBEAT_OK"

   # Evening sync at 11pm
   openclaw cron add --schedule "0 23 * * *" --text \
     "Run the pre-commit sync for the vault at $VAULT. Read CLAUDE.md for conventions, then read and execute the workflow in .claude/commands/sync.md. Follow every step exactly as documented."

   # Weekly review Sunday 6pm
   openclaw cron add --schedule "0 18 * * 0" --text \
     "Run the weekly review for the vault at $VAULT. Read CLAUDE.md for conventions, then read and execute the workflow in .claude/commands/weekly-review.md. Follow every step exactly — including daily note archiving, bloated note cleanup, monthly rollup (if applicable), and orphan detection."
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

Slash commands are already set up in `.claude/commands/`. No additional configuration needed.

### Available Commands

| Command | File | What It Does |
|---------|------|-------------|
| `/project:morning-briefing` | `.claude/commands/morning-briefing.md` | Create daily note, summarize yesterday, surface tasks |
| `/project:inbox` | `.claude/commands/inbox.md` | Triage items in 0-Inbox/ |
| `/project:sync` | `.claude/commands/sync.md` | Review daily note, check consistency, commit & push |
| `/project:weekly-review` | `.claude/commands/weekly-review.md` | Deep clean, archive, synthesize, monthly rollup |

### Usage

```bash
cd /path/to/vault
claude
> /project:morning-briefing
> /project:inbox
> /project:sync
> /project:weekly-review
```

To customize a workflow, edit the corresponding file in `.claude/commands/`. Changes automatically apply to both manual slash commands and cron jobs (since cron payloads reference these files).

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
