# Morning Briefing

Start the day with context.

## Steps

1. **Check today's daily note:**
   - If `1-Daily/YYYY-MM-DD.md` doesn't exist, create it from `_templates/daily.md`
   - Replace `{{date:YYYY-MM-DD}}` with today's date
   - Replace `{{date:dddd}}` with day name (Monday, Tuesday, etc.)

2. **Read yesterday's daily note:**
   - Extract key accomplishments from "✅ Done Today"
   - Note any open questions from "🤖 AI Sync"

3. **Check active projects:**
   - Look in `2-Projects/` for folders
   - Read each project's `README.md`
   - List projects with status 🟡 (In Progress) or 🟢 (Active)
   - Flag any with tasks not updated in 7+ days

4. **Summarize:**
   Output a brief morning summary with:
   - Yesterday's highlights (2-3 bullets)
   - Active projects needing attention
   - Any open questions or blockers
   - Suggested focus for today

**Keep it concise — aim for 10 lines max.**
