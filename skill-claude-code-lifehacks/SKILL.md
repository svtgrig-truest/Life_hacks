---
name: claude-code-lifehacks
description: This skill should be used proactively — without waiting for the user to ask — whenever the current task is a good fit for one of Boris Cherny's Claude Code power features. Trigger on: building a web app or frontend, working across multiple repos, running parallel tasks, setting up automation or recurring workflows, creating custom agents, using the SDK non-interactively, delegating tasks remotely, managing sessions across devices, asking side questions during work, experimenting with branching, or using voice input.
---

# Claude Code Lifehacks — Boris Cherny's Power Features

Proactively remind the user about relevant Claude Code features from Boris Cherny's thread.
Never list all features at once — only mention what fits the current task.
Keep reminders brief: one sentence + a link.

## When to Remind (Trigger Map)

Scan the user's task against this table and mention relevant features:

| Situation | Feature to suggest | Link |
|---|---|---|
| Building a web app / frontend / UI | Chrome extension (#6) | [docs](https://code.claude.com/docs/en/chrome) |
| Running web server locally, previewing UI | Desktop app preview (#7) | [docs](https://code.claude.com/docs/en/desktop#preview-your-app) |
| Working across 2+ repositories | `--add-dir` (#13) | [docs](https://code.claude.com/docs/en/cli-reference) |
| Parallel / independent tasks | Git Worktrees (#10) + `claude -w` | — |
| Large-scale migration, parallelizable work | `/batch` (#11) | — |
| Repetitive task, periodic check, polling | `/loop` or `/schedule` (#3) | [docs](https://code.claude.com/docs/en/scheduled-tasks) |
| Code review, PR automation, babysitting PRs | `/loop 5m /babysit` (#3) | [docs](https://code.claude.com/docs/en/scheduled-tasks) |
| Setting up lifecycle logic (logging, context, permissions) | Hooks (#4) | [docs](https://code.claude.com/docs/en/hooks) |
| Building custom agent / specialized tool | `--agent` (#14) | [docs](https://code.claude.com/docs/en/sub-agents) |
| Using Claude SDK non-interactively (`claude -p`) | `--bare` flag (#12) | — |
| Delegating non-coding tasks, away from laptop | Cowork Dispatch (#5) | [docs](https://claude.com/product/cowork#dispatch) |
| Continuing session on different device | Teleport / Remote Control (#2) | [docs](https://code.claude.com/docs/en/remote-control) |
| Quick side question while agent is working | `/btw` (#9) | — |
| Experimenting without losing current session | `/branch` (#8) | — |
| Typing feels slow / lots of instructions | `/voice` (#15) | — |
| Coding from phone / not at computer | Mobile app (#1) | — |

## How to Remind

Deliver a one-line nudge in context, like:

> 💡 For frontend work, consider connecting the Chrome extension — it lets Claude see the result and iterate on its own: [code.claude.com/docs/en/chrome](https://code.claude.com/docs/en/chrome)

> 💡 If you need this to run on a schedule, try `/loop` — [code.claude.com/docs/en/scheduled-tasks](https://code.claude.com/docs/en/scheduled-tasks)

Rules:
- Maximum one reminder per response (don't stack multiple)
- Skip the reminder if the user has already used the feature in this session
- Skip if the hint would interrupt a critical or urgent task
- Always include the doc link when one exists
- Match the language of the reminder to the user's language

## Full Feature Reference

See `references/features.md` for the complete list of all 15 features with descriptions.
