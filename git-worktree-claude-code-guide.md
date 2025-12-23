# Git + Claude Code: Complete Workflow Guide

A practical guide from starting a project to finishing it with Claude Code.

---

## Table of Contents

1. [Project Setup](#1-project-setup)
2. [Start Working](#2-start-working)
3. [Write Code with Claude](#3-write-code-with-claude)
4. [Test Your Code](#4-test-your-code)
5. [Commit Changes](#5-commit-changes)
6. [Create Pull Request](#6-create-pull-request)
7. [Code Review](#7-code-review)
8. [Approve & Merge PR](#8-approve--merge-pr)
9. [Cleanup](#9-cleanup)
10. [Advanced: Parallel Work with Worktrees](#10-advanced-parallel-work-with-worktrees)
11. [Quick Reference](#11-quick-reference)

---

## 1. Project Setup

### Initialize your repository

```bash
# Create new project
mkdir my-project && cd my-project
git init

# Or clone existing
git clone https://github.com/user/repo.git
cd repo
```

### Create CLAUDE.md (recommended)

This file tells Claude how to work in your project:

```bash
# Create the file
touch CLAUDE.md
```

Add these basics:

```markdown
# Project Guidelines

## Git Workflow
- Always create feature branches
- Use /commit-commands:commit after completing tasks
- Use /commit-commands:commit-push-pr to create PRs

## Commit Format
- feat: new feature
- fix: bug fix
- docs: documentation
- test: adding tests
```

---

## 2. Start Working

### Rule #1: Never work on main

```bash
# ❌ Bad
git checkout main
claude

# ✅ Good
git checkout -b feature/login-page
claude
```

### Create a feature branch

```bash
git checkout -b feature/your-feature-name
```

### Start Claude Code

```bash
claude
```

### Name your session (optional but helpful)

```
> /rename login-feature
```

---

## 3. Write Code with Claude

### Ask Claude to implement features

```
> add a login form with email and password validation
> create a user authentication module
> add error handling to the API calls
```

### Best practice: Ask for tests together

```
> add login validation AND write tests for it
```

---

## 4. Test Your Code

### Run tests before committing

```
> run the tests
> fix any failing tests
```

### When to test

| When | What | Who |
|------|------|-----|
| Before commit | Unit tests pass | You/Claude |
| After PR created | Full test suite | CI/CD (automatic) |
| During review | Test coverage | Reviewer |

---

## 5. Commit Changes

### Use the commit skill

```
> /commit-commands:commit
```

### Or commit manually with good messages

```
> commit with message "feat(auth): add login validation"
```

### Commit message format

```
type(scope): description

Examples:
- feat(auth): add login page
- fix(api): handle null response
- docs(readme): update install steps
- test(user): add registration tests
```

---

## 6. Create Pull Request

### Quick way (recommended)

```
> /commit-commands:commit-push-pr
```

This does everything: commit → push → create PR

### Or step by step

```
> commit these changes
> push to remote
> create a pr with title "Add login feature"
```

### When to use PRs?

| Situation | Use PR? |
|-----------|---------|
| Team project | ✅ Yes |
| Production code | ✅ Yes |
| Solo project | Optional |
| Quick experiment | ❌ No |

---

## 7. Code Review

### Request a review

```
> /code-review:code-review
```

### What reviewers check

- Does the code work?
- Are there tests?
- Are edge cases handled?
- Is it secure?

### CI/CD runs automatically

After you create a PR, GitHub Actions (or similar) runs:
- All tests
- Linting
- Security checks

### Approve a PR from Claude Code

```
> approve PR #123
> gh pr review 123 --approve
> gh pr review 123 --approve --body "Looks good!"
```

### Request changes

```
> gh pr review 123 --request-changes --body "Please fix the validation"
```

### View PR details

```
> show me PR #123
> gh pr view 123
> gh pr diff 123
```

---

## 8. Approve & Merge PR

### Merge options

```bash
# Regular merge (keeps all commits)
> gh pr merge 123 --merge

# Squash merge (combines into one commit) - recommended
> gh pr merge 123 --squash

# Rebase merge (linear history)
> gh pr merge 123 --rebase
```

### Full workflow example

```
> show me PR #123              # View the PR
> review the changes           # Check the code
> approve PR #123              # Approve it
> gh pr merge 123 --squash     # Merge it
```

### PR commands reference

| Command | What it does |
|---------|--------------|
| `gh pr list` | List open PRs |
| `gh pr view 123` | View PR details |
| `gh pr diff 123` | See PR changes |
| `gh pr review 123 --approve` | Approve PR |
| `gh pr review 123 --request-changes` | Request changes |
| `gh pr merge 123 --squash` | Squash and merge |
| `gh pr close 123` | Close without merging |

---

## 9. Cleanup

### After PR is merged

1. Delete the remote branch (GitHub offers this option)
2. Clean up locally:

```bash
git checkout main
git pull
git branch -d feature/your-feature-name
```

### Clean up old branches

```
> /commit-commands:clean_gone
```

This removes branches deleted on remote.

---

## 10. Advanced: Parallel Work with Worktrees

### What are worktrees?

Work on **multiple branches at the same time** in separate folders.

```
my-project/           ← main branch
my-project-feature/   ← feature branch (worktree)
my-project-bugfix/    ← bugfix branch (worktree)
```

### Why use worktrees?

| Without Worktrees | With Worktrees |
|-------------------|----------------|
| One branch at a time | Multiple branches |
| Must stash to switch | No stashing needed |
| One Claude session | Multiple Claude sessions |

### How to use

**Create a worktree:**
```bash
git worktree add ../my-project-feature -b feature/new-thing
```

**Work in it:**
```bash
cd ../my-project-feature
claude
```

**Run multiple Claude sessions:**
```bash
# Terminal 1
cd ../my-project-feature && claude

# Terminal 2
cd ../my-project-bugfix && claude
```

**Clean up when done:**
```bash
git worktree remove ../my-project-feature
```

### Worktree commands

```bash
# Create with new branch
git worktree add <path> -b <branch-name>

# Create from existing branch
git worktree add <path> <existing-branch>

# List all worktrees
git worktree list

# Remove worktree
git worktree remove <path>

# Force remove (loses uncommitted changes!)
git worktree remove --force <path>
```

### Why worktrees beat cloning

1. **Saves disk space** — shares .git folder
2. **Stays synced** — one `git fetch` updates all
3. **Instant creation** — no network needed

---

## 11. Quick Reference

### Complete Workflow

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

### Claude Code Skills

| Skill | What it does |
|-------|--------------|
| `/commit-commands:commit` | Commit changes |
| `/commit-commands:commit-push-pr` | Commit + push + create PR |
| `/code-review:code-review` | Review code |
| `/commit-commands:clean_gone` | Cleanup old branches |

### Session Management

```bash
# Name your session
> /rename my-feature

# Resume later
claude --resume my-feature

# Session picker shortcuts
↑/↓  Navigate
Enter  Select
B  Filter by branch
P  Preview
```

### Git Commands

```bash
# Branches
git checkout -b feature/name    # Create branch
git branch -d branch-name       # Delete branch

# Worktrees
git worktree add <path> -b <branch>  # Create
git worktree list                     # List all
git worktree remove <path>            # Remove
```

---

## References

- [Git Worktree Documentation](https://git-scm.com/docs/git-worktree)
- [Claude Code Workflows](https://docs.anthropic.com/en/docs/claude-code/common-workflows)
