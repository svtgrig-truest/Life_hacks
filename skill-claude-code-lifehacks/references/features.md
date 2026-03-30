# 15 Hidden Claude Code Features — Boris Cherny

Source: https://x.com/bcherny/status/2038454336355999749

## 1. Mobile App
Claude Code has a mobile app for iOS/Android. Review PRs, write code from your phone.

## 2. Teleport / Remote Control
`claude --teleport` or `/teleport` — pull a cloud session down to your local terminal.
`/remote-control` — control a local session from your phone or browser.
Docs: https://code.claude.com/docs/en/remote-control

## 3. /loop and /schedule
Schedule Claude to run automatically at set intervals (up to a week).
Boris's examples:
- `/loop 5m /babysit` — code review, rebase, shepherd PRs to production
- `/loop 30m /slack-feedback` — auto-create PRs from Slack feedback
- `/loop /post-merge-sweeper` — PRs for missed code review comments
- `/loop 1h /pr-pruner` — close stale PRs
Docs: https://code.claude.com/docs/en/scheduled-tasks

## 4. Hooks
Deterministic logic in the agent lifecycle:
- `SessionStart` — load context on startup
- `PreToolUse` — log bash commands
- `PermissionRequest` — route permission prompts to WhatsApp
- `Stop` — nudge Claude to keep going
Docs: https://code.claude.com/docs/en/hooks

## 5. Cowork Dispatch
Secure remote control for Claude Desktop. Delegate non-coding tasks from anywhere.
Link: https://claude.com/product/cowork#dispatch

## 6. Chrome Extension
Give Claude a way to see the result of its work — it will iterate until the result is great.
Docs: https://code.claude.com/docs/en/chrome

## 7. Desktop App — Web Server Preview
Desktop automatically runs your web server and tests it in a built-in browser.
Docs: https://code.claude.com/docs/en/desktop#preview-your-app

## 8. Fork Session (/branch)
`/branch` — branch a conversation without losing the original.
`claude --resume <id> --fork-session` — fork from CLI.

## 9. /btw
Ask a side question without interrupting the agent: `/btw how do I spell dachshund?`

## 10. Git Worktrees
`claude -w` — new session in a worktree. Boris runs dozens of instances simultaneously.
Use the `WorktreeCreate` hook for non-git VCS.

## 11. /batch
Fans out work to thousands of worktree agents. Ideal for large-scale migrations.

## 12. --bare
`claude -p ... --bare` — up to 10x faster SDK startup (skips CLAUDE.md and MCP discovery).

## 13. --add-dir
`--add-dir /path/to/other-repo` or `/add-dir` — grant access to additional folders.
Or add `"additionalDirectories"` to `settings.json`.
Docs: https://code.claude.com/docs/en/cli-reference

## 14. --agent
`.claude/agents/` + `claude --agent=<name>` — custom system prompt and tools.
Docs: https://code.claude.com/docs/en/sub-agents

## 15. /voice
Boris dictates most of his code by voice. `/voice` in CLI → hold space to speak.
