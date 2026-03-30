# Installation

Copy the `skill-claude-code-lifehacks/` directory into your Claude Code skills folder:

```bash
cp -r skill-claude-code-lifehacks ~/.claude/skills/claude-code-lifehacks
```

Claude Code will pick it up automatically on next launch.

## What it does

Proactively reminds you to use Boris Cherny's Claude Code power features when your current task is a good fit — one nudge at a time, never intrusive.

## Optional: daily auto-update via scheduled task

To auto-check Boris Cherny's X profile for new lifehacks and update the skill automatically, create a scheduled task in Claude Code with the prompt in `scheduled-task-prompt.md`.
Replace `<YOUR_SKILLS_DIR>` with your actual `~/.claude/skills` path.
