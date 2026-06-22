# monacori

**Validation control plane for AI-generated code changes.** After an AI edits your repository, `monacori` produces verification evidence a human can actually trust.

It is *not* an agent orchestrator. It does not manage panes, sessions, worktrees, or model adapters. Its job is narrow on purpose: validate what the AI just did.

## Why

AI coding output is hard to trust when review depends on chat memory or a vague "done" claim. `monacori` keeps the review artifacts inside the repository, so the state of a change can be inspected, rerun, and discussed instead of taken on faith.

The loop is simple:

```text
AI edits code.
monacori runs verification.
monacori creates a reviewable diff artifact.
You inspect the evidence before accepting the change.
```

## Install

```bash
npm install -g @happy-nut/monacori
```

After install, the short command is `mo`. A Homebrew tap (`happy-nut/monacori/monacori`) is also available.

## What you get

- **Local desktop review app** — diff review with changed-line highlighting and an IntelliJ-style sidebar that colors files by git status. Reads the repo directly, refreshes on change, no HTTP server.
- **Integrated terminal** — run AI CLIs like `claude` or `codex` inside the app, and send a "merged prompt" (your question or fix request bundled with the relevant code context) straight to the session.
- **Inline comments** — annotate the diff while you review.
- **Verification logs & reports** — repeatable verification under `.monacori/logs/` and compact validation reports under `.monacori/reports/`.

## Quick start

Inside the repository you want to validate:

```bash
mo                              # open the desktop review app for the current dir
monacori check --include-untracked   # run verification, write a log, diff, and report
```

On first run, `mo` creates `.monacori/`, adds it to `.gitignore`, and includes untracked files so new AI-created files show up immediately.

## Commands

| Command | What it does |
| --- | --- |
| `mo` | Open the desktop review app (alias for `monacori open`). |
| `monacori check` | Run verification, then create a diff and a validation report. `-- <cmd>` overrides commands for one run. |
| `monacori verify` | Run configured verification commands and store the log. Exits non-zero on failure. |
| `monacori diff` | Generate a browser-based side-by-side diff page. `--watch` serves a live-reloading review. |
| `monacori app` | Launch the desktop review app (same as `mo`). |
| `monacori report` | Store a manual report under `.monacori/reports/`. |
| `monacori status` | Print branch, git status, diff stat, verification commands, and recent reports/logs. |

## Repository state

`monacori init` (run automatically by `mo`) creates:

```text
.monacori/
  config.json   verification commands and diff defaults
  state.md      compact validation history
  diffs/        generated browser diff reviews
  reports/      validation reports
  logs/         verification logs
```

Keep `.monacori/` ignored unless your team explicitly wants to commit validation state.

## Design principles

- Verification evidence beats chat memory.
- Generated artifacts are plain Markdown, JSON, logs, or static HTML.
- No required AI agent, terminal multiplexer, editor, or worktree strategy.
- The default command should be useful after any AI-generated edit.
- A change is not accepted until the evidence is clear or the gap is documented.

## License

MIT
