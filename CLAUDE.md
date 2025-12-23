# Project Guidelines

## Git Workflow

After completing a task:
1. Commit changes using `/commit-commands:commit`
2. Push and create PR with `/commit-commands:commit-push-pr` if requested

## Commit Message Format

Use conventional commits:

| Type | Description |
|------|-------------|
| feat | New feature |
| fix | Bug fix |
| docs | Documentation changes |
| refactor | Code refactoring |
| test | Adding or updating tests |
| chore | Maintenance tasks |

Format: `type(scope): description`

Examples:
- `feat(auth): add login functionality`
- `fix(api): handle null response`
- `docs(readme): update installation steps`

## Commit Rules

- One logical change per commit
- Keep commits atomic and reviewable
- Write clear, descriptive messages
- Reference issue numbers when applicable: `Fixes #123`
