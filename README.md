# AI Coding Workflow Guide

A practical guide for using Git with Claude Code and AI coding assistants — from project setup to PR merge.

## What's Inside

| File | Description |
|------|-------------|
| [git-worktree-claude-code-guide.md](git-worktree-claude-code-guide.md) | Complete workflow guide |
| [CLAUDE.md](CLAUDE.md) | Project guidelines template |

## Quick Start

1. Copy `CLAUDE.md` to your project root
2. Follow the workflow in the guide
3. Use the quick reference for commands

## Workflow Overview

```
┌──────────────────────────────────────────────────┐
│  1. git checkout -b feature/name                 │
├──────────────────────────────────────────────────┤
│  2. claude                                       │
├──────────────────────────────────────────────────┤
│  3. > implement feature and write tests          │
├──────────────────────────────────────────────────┤
│  4. > run tests                                  │
├──────────────────────────────────────────────────┤
│  5. > /commit-commands:commit-push-pr            │
├──────────────────────────────────────────────────┤
│  6. > /code-review:code-review                   │
├──────────────────────────────────────────────────┤
│  7. > gh pr review 123 --approve                 │
├──────────────────────────────────────────────────┤
│  8. > gh pr merge 123 --squash                   │
├──────────────────────────────────────────────────┤
│  9. > /commit-commands:clean_gone                │
└──────────────────────────────────────────────────┘
```

## Topics Covered

- **Project Setup** — Initialize repo, create CLAUDE.md
- **Branching** — Always use feature branches
- **Development** — Write code with Claude
- **Testing** — Test before commit
- **Commits** — Conventional commit format
- **Pull Requests** — Create, review, approve, merge
- **Code Review** — Using Claude for reviews
- **Cleanup** — Remove merged branches
- **Worktrees** — Parallel development (advanced)

## Key Commands

| Command | What it does |
|---------|--------------|
| `/commit-commands:commit` | Commit changes |
| `/commit-commands:commit-push-pr` | Commit + push + create PR |
| `/code-review:code-review` | Review code |
| `/commit-commands:clean_gone` | Cleanup old branches |
| `gh pr review 123 --approve` | Approve a PR |
| `gh pr merge 123 --squash` | Merge a PR |

## Requirements

- [Claude Code](https://claude.com/claude-code) CLI
- [GitHub CLI](https://cli.github.com/) (`gh`)
- Git

## License

MIT — Use freely, modify as needed.

---

**Generated with [Claude Code](https://claude.com/claude-code)**
