# AI Workspace Setup Guide

*How to build an integrated environment where AI assistants become effective collaborators.*

---

## The Big Picture

Your AI workspace has four layers:

```
┌─────────────────────────────────────────────────────┐
│ 1. Global Instructions (CLAUDE.md / AGENTS.md)      │  ← How to behave everywhere
│    ~/.claude/CLAUDE.md                              │
└─────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────┐
│ 2. Project Instructions (CLAUDE.md)                 │  ← How to work with THIS vault
│    /vault/CLAUDE.md                                 │
└─────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────┐
│ 3. Long-term Memory (MEMORY.md)                     │  ← What we've learned/decided
│    /vault/MEMORY.md or project-specific             │
└─────────────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────────────┐
│ 4. Skills & Workflows                               │  ← Reusable procedures
│    .claude/commands/ or custom skills/              │
└─────────────────────────────────────────────────────┘
```

---

## Layer 1: Global Instructions

**File:** `~/.claude/CLAUDE.md`

Your universal AI instruction set — rules that apply everywhere.

```markdown
# Global AI Instructions

## About Me
I'm [name], a [role] who prefers:
- Concise communication
- Ask before making big changes
- Explain trade-offs when suggesting alternatives

## Boundaries
### Do Freely:
- Read files, explore, organize
- Run tests, create branches

### Ask First:
- Push to main, delete files
- Send external communications
```

### Setup

```bash
mkdir -p ~/.claude
# Create your global instructions
vim ~/.claude/CLAUDE.md
```

---

## Layer 2: Project Instructions

**File:** `/vault/CLAUDE.md` (included in this template)

Teaches AI about this specific vault — structure, conventions, workflows.

This template includes a complete CLAUDE.md. Customize it for your preferences.

---

## Layer 3: Long-term Memory

**File:** `/vault/MEMORY.md` or project-specific

Where context persists across sessions.

```markdown
# Vault Memory

## Key Decisions

### 2026-01-15: Chose PARA over Zettelkasten
**Reasoning:** More intuitive for project-based work.
**Trade-off:** Less serendipitous discovery.

## Preferences
- Daily notes: Morning review, evening wrap-up
- Projects: Always have README + tasks at minimum
- Archives: Monthly for daily notes

## Lessons Learned
- Weekly reviews on Sundays work better than Fridays
- Keep 4-Resources flat — 2 levels max
```

### When to Update

Add to MEMORY.md after:
- Making an important decision
- Learning something non-obvious
- Establishing a new convention
- Completing a significant project

---

## Layer 4: Skills & Workflows

**Location:** `.claude/commands/`

Packaged instructions for specific tasks.

### Example: Morning Briefing

**File:** `.claude/commands/morning-briefing.md`

```markdown
# Morning Briefing

1. Check if today's daily note exists → create if not
2. Read yesterday's daily note
3. Check active projects
4. Summarize in 10 lines max
```

### Using Skills

**Claude Code:**
```bash
claude
> /project:morning-briefing
```

**Conversation:**
```
You: "Run the morning briefing"
AI: [Follows the skill instructions]
```

This template includes ready-to-use skills in `.claude/commands/`.

---

## Tool Compatibility

| Tool | Config Location | Notes |
|------|-----------------|-------|
| Claude Code | `CLAUDE.md` | Native support |
| OpenCode | `AGENTS.md` | Copy CLAUDE.md → AGENTS.md |
| Cursor | `.cursorrules` | Copy CLAUDE.md |
| Clawdbot | `CLAUDE.md` | Full automation support |
| Aider | CLI flag | `aider --read CLAUDE.md` |

---

## Quick Start

1. **Fork this template**
2. **Set up global instructions:**
   ```bash
   mkdir -p ~/.claude
   vim ~/.claude/CLAUDE.md
   # Add your personal preferences
   ```
3. **Customize vault CLAUDE.md** if needed
4. **Create your first daily note**
5. **Start using!**
   ```bash
   claude  # or your preferred tool
   > /project:morning-briefing
   ```

---

## Best Practices

### Writing Instructions

**Do:**
- ✅ Be specific: "Use YYYY-MM-DD format" not "date your notes"
- ✅ Use examples: Show what good notes look like
- ✅ Keep it under 300 lines total
- ✅ Update when you notice gaps

**Don't:**
- ❌ Be vague: "Keep it organized"
- ❌ Over-instruct: LLMs ignore excessive rules
- ❌ Duplicate: Link to docs, don't copy them

### Growing Memory

**Add when:**
- You make a decision
- You learn something non-obvious
- You establish a convention

**Review:**
- Monthly: Archive stale info
- Quarterly: Major cleanup

### Creating Skills

**Good skill topics:**
- Daily workflows (morning, evening)
- Maintenance tasks (review, archive)
- Project operations (create, close)

**Quality checklist:**
- [ ] Clear prerequisites
- [ ] Step-by-step instructions
- [ ] Error handling notes
- [ ] Tested with AI

---

## Troubleshooting

### "AI doesn't follow instructions"

1. **Too many instructions** — Keep under 200
2. **Too vague** — Be specific with examples
3. **File not being read** — Check location matches your tool

### "AI forgets context"

1. Update MEMORY.md after important sessions
2. Document in project files
3. Use session handoff in daily notes

### "Slash commands don't work"

- Must be in `.claude/commands/`
- Files must be `*.md`
- Access as `/project:name`

---

## Resources

- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)
- [Writing a Good CLAUDE.md](https://www.humanlayer.dev/blog/writing-a-good-claude-md)
- [AGENTS.md Standard](https://agents.md/)
- [Clawdbot](https://github.com/clawdbot/clawdbot)

---

*For the full comprehensive guide with all details, see the [complete AI Workspace Setup Guide](https://github.com/your-repo/docs/full-guide.md).*
