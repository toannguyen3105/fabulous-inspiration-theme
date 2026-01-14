---
description: Standard Git Feature Development Flow
---

# Git Feature Workflow

This workflow standardizes the process of starting and finishing a feature using Git, ensuring a clean history and correct branching strategy.

## Usage

Start a new feature:

```
/git-flow start [feature-name]
```

Commit changes:

```
/git-flow commit
```

Finish feature (Push & PR):

```
/git-flow finish
```

## Steps

### Start Branch

1.  **Identify Type**: Ask user if this is a **New Feature** or **Bug Fix**.
    - If Feature: Use prefix `feature/`
    - If Bug Fix: Use prefix `fix/` (or `hotfix/` if critical on production)
2.  **Switch to Main**: `git checkout main`
3.  **Fetch & Pull Main**: `git pull origin main`
4.  **Sync Develop**:
    - Fetch latest: `git fetch origin develop`
    - Checkout develop: `git checkout develop` || `git checkout -b develop origin/develop`
    - **Reset Hard**: `git reset --hard origin/develop` (Ensure local develop matches server exactly).
5.  **Update Develop with Main**:
    - Command: `git merge main`
    - _Check_: If merge fails (conflict), **STOP** and notify user to resolve conflicts manually.
6.  **Create Branch**: Create a new branch `[prefix]/[name]` from `develop`.

    - Command: `git checkout -b [prefix]/[name]`
    - _Validation_: Ensure `name` is kebab-case.

7.  **Conflict Handling (If Step 5 Fails)**:
    - **Status Check**: Run `git status` to see conflicted files.
    - **Manual Fix**: Edit files to resolve conflicts (look for `<<<<<<< HEAD`).
    - **Continue**:
      - Stage fixes: `git add .`
      - Complete merge: `git commit -m "Merge branch 'main' into develop"`
      - **Retry Sync**: Return to Step 6 to create your branch.

### Commit Changes

1.  **Stage Files**: `git add .`
2.  **Generate Message**: Analyze changes and format the message using strict Conventional Commits:
    - **feat**: for new features (e.g., `feat: add new hero section`)
    - **fix**: for bug fixes (e.g., `fix: correct typo in header`)
    - **hotfix**: for critical production fixes (e.g., `hotfix: patch security vulnerability`)
3.  **Commit**: `git commit -m "[type]: [concise message]"`

### Finish Feature

1.  **Push Branch**: `git push -u origin [current-branch]`
2.  **Create PR**: Use `gh pr create` (GitHub CLI) to open a Pull Request into `develop`.
    - _Prompt_: Ask for PR title and body if not provided.

### Cleanup (After PR Merge)

1.  **Switch to Develop**: `git checkout develop`
2.  **Pull Latest**: `git pull origin develop`
3.  **Delete Local Branch**: `git branch -d [branch-name]`
4.  **Delete Remote Branch**:
    - _Option 1_: GitHub automatically deletes head branch on merge (Recommended setting).
    - _Option 2_: Manual command: `git push origin --delete [branch-name]`

## Automation

- Use `// turbo` for `git checkout`, `git pull` commands where safe to avoid excessive confirmations.
