# monacori

**A local desktop diff-review app for AI-generated code changes.** After an AI edits your repo, run `mo` to open a side-by-side diff — read it, comment on it, and send your comments straight to an AI CLI running in the built-in terminal.

## Why

A chat log or a "done" claim is a poor way to review what an AI changed. monacori puts the change in front of you as a real diff you can read and annotate — then turns your comments into a prompt you hand right back to `claude` or `codex`, without leaving the app or copy-pasting between windows.

## Install

```bash
npm install -g @happy-nut/monacori
```

After install, the short command is `mo`. A Homebrew tap (`happy-nut/monacori/monacori`) is also available.

## What you get

- **Desktop diff review** — side-by-side diff with changed-line highlighting and an IntelliJ-style sidebar that colors files by git status. Reads the repo directly, refreshes on change, no HTTP server.
- **Integrated terminal** — run AI CLIs like `claude` or `codex` right inside the app, split into panes.
- **Comments → session** — annotate any line, then send your comments (bundled with their code context) into a terminal pane as one merged prompt: pick the target pane visually and press Enter.

## Quick start

Inside the repository you want to review:

```bash
mo
```

On first run, `mo` creates `.monacori/`, adds it to `.gitignore`, and includes untracked files so new AI-created files show up immediately.

## Commands

| Command | What it does |
| --- | --- |
| `mo` | Open the desktop diff-review app (alias for `monacori open`). |
| `monacori app` | Launch the desktop review app (same as `mo`). |
| `monacori init` | Initialize `.monacori/` in the current directory. |
| `monacori install` | Initialize and write agent instruction snippets. `--apply-agent-docs` patches `AGENTS.md` / `CLAUDE.md`. |

## Repository state

`monacori init` (run automatically by `mo`) creates a git-ignored `.monacori/` directory holding generated diff reviews and local config. Keep it ignored unless your team explicitly wants to commit review state.

## Design principles

- A real diff beats a chat log or a "done" claim.
- Review, comment, and hand-off live in one window — no copy-paste loop.
- Generated artifacts are plain static HTML and JSON.
- No required AI agent, terminal multiplexer, editor, or worktree strategy.

## License

MIT
