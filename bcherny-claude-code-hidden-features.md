# 16 Hidden & Under-Utilized Features in Claude Code

**Author:** Boris Cherny ([@bcherny](https://x.com/bcherny)), creator of Claude Code
**Date:** March 30, 2026
**Source:** [X (Twitter)](https://x.com/bcherny/status/2038454336355999749)

---

## 1. Mobile App

Claude Code has a mobile app. Boris writes a lot of his code from the iOS app — a convenient way to make changes without opening a laptop.

- Download the Claude app for iOS/Android
- Navigate to the **Code** tab on the left
- Review changes, approve PRs, and write code directly from your phone

---

## [2. Move Sessions Between Mobile/Web/Desktop and Terminal](https://code.claude.com/docs/en/remote-control)

Run `claude --teleport` or `/teleport` to continue a cloud session locally. Or run `/remote-control` to control a locally running session from your phone or browser.

- **Teleport** — pulls a cloud session down to your local terminal
- **Remote Control** — lets you control a local session from any device
- Boris has "Enable Remote Control for all sessions" set in his `/config`

---

## [3. /loop and /schedule — Two of the Most Powerful Features](https://code.claude.com/docs/en/scheduled-tasks)

Schedule Claude to run automatically at a set interval for up to a week. Boris runs multiple loops locally:

- `/loop 5m /babysit` — auto-address code review, auto-rebase, and shepherd PRs to production
- `/loop 30m /slack-feedback` — automatically put up PRs for Slack feedback every 30 minutes
- `/loop /post-merge-sweeper` — put up PRs to address missed code review comments
- `/loop 1h /pr-pruner` — close out stale and unnecessary PRs

Tip: turn your workflows into skills and combine them with loops.

---

## [4. Hooks for Deterministic Logic](https://code.claude.com/docs/en/hooks)

Hooks run logic as part of the agent lifecycle:

- **Dynamically load context** each time you start Claude (`SessionStart`)
- **Log every bash command** the model runs (`PreToolUse`)
- **Route permission prompts** to WhatsApp for you to approve/deny (`PermissionRequest`)
- **Poke Claude** to keep going whenever it stops (`Stop`)

---

## [5. Cowork Dispatch](https://claude.com/product/cowork#dispatch)

Boris uses Dispatch every day to catch up on Slack and emails, manage files, and do things on his laptop when he's not at a computer.

- Dispatch is a **secure remote control** for the Claude Desktop app
- It can use your MCPs, browser, and computer, with your permission
- Delegate non-coding tasks to Claude from anywhere

---

## [6. Chrome Extension for Frontend Work](https://code.claude.com/docs/en/chrome)

**Key principle:** give Claude a way to verify its output. Once you do that, Claude will iterate until the result is great.

- Without a browser, website-building results likely won't look good
- With a browser, Claude writes code and iterates until it looks good
- Boris uses the Chrome extension every time he works on web code — it outperforms similar MCPs

---

## [7. Desktop App to Auto-Start and Test Web Servers](https://code.claude.com/docs/en/desktop#preview-your-app)

The Desktop app bundles in the ability for Claude to automatically run your web server and test it in a built-in browser.

- Set up something similar in CLI or VSCode using the Chrome extension
- Or use the Desktop app for the integrated experience

---

## 8. Fork Your Session

Two ways to branch an existing session:

1. Run `/branch` from your session
2. From CLI: `claude --resume <session-id> --fork-session`

`/branch` creates a branched conversation. Resume the original with `claude -r <original-session-id>`.

---

## 9. /btw — Side Queries Without Interrupting the Agent

The `/btw` command lets you ask a side question while the agent works without interrupting its current task.

Example: `/btw how do I spell dachshund?` — you get an immediate answer and work continues.

---

## 10. Git Worktrees

Claude Code has deep git worktree support — essential for parallel work in the same repository. Boris runs dozens of Claude instances simultaneously.

- `claude -w` — start a new session in a worktree
- Check the "worktree" checkbox in Claude Desktop
- For non-git VCS: use the `WorktreeCreate` hook for custom logic

---

## 11. /batch — Fan Out Massive Changesets

`/batch` interviews you, then fans out work to dozens, hundreds, or even thousands of worktree agents simultaneously.

- Ideal for large code migrations and parallelizable work
- Each agent works independently on its own copy of the codebase

---

## 12. --bare — Speed Up SDK Startup by Up to 10x

By default, `claude -p` searches for local CLAUDE.md files, settings, and MCPs. For non-interactive use, explicitly specify what to load.

- This was a design oversight when the SDK was first built
- A future version will flip the default to `--bare`
- Opt in now for up to **10x faster startup**

```bash
claude -p "summarize this codebase" \
    --output-format=stream-json \
    --verbose \
    --bare
```

---

## [13. --add-dir — Give Claude Access to More Folders](https://code.claude.com/docs/en/cli-reference)

When working across multiple repositories, start Claude in one repo and use `--add-dir` (or `/add-dir`) to let Claude see the others.

- Tells Claude about the repo and gives it permissions to work there
- Add `"additionalDirectories"` to your team's `settings.json` to always load additional folders

---

## [14. --agent — Custom System Prompt & Tools](https://code.claude.com/docs/en/sub-agents)

Define custom agents in `.claude/agents/`, then run:

```bash
claude --agent=<your agent's name>
```

- Agents can have restricted tools, custom descriptions, and specific models
- Great for read-only agents, specialized review agents, or domain-specific tools

---

## 15. /voice — Voice Input

Boris does most of his coding by speaking to Claude rather than typing.

- In CLI: run `/voice`, then hold the space bar to speak
- In Desktop: press the voice button
- On iOS: enable dictation in settings

---

## [16. "if" Conditions in Hooks — Conditional Hook Execution](https://code.claude.com/docs/en/hooks)

Add an `"if"` field to any hook handler to filter execution to specific commands. The hook only spawns a subprocess when both the matcher **and** the `if` condition match — saving significant time in long sessions.

- `"if": "Bash(git *)"` — run only for git commands
- `"if": "Edit(*.ts)"` — run only when editing TypeScript files
- `"if": "Bash(rm *)"` — run only for rm commands
- Works with: `PreToolUse`, `PostToolUse`, `PostToolUseFailure`, `PermissionRequest`

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "if": "Bash(git *)",
            "command": ".claude/hooks/git-security-check.sh"
          }
        ]
      }
    ]
  }
}
```

*Retweeted by Boris Cherny from @jarredsumner, March 27, 2026*
