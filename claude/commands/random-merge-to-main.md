---
description: Merge current branch into main and delete the branch.
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git rev-parse:*), Bash(git branch:*), Bash(git checkout:*), Bash(git switch:*), Bash(git pull:*), Bash(git merge:*), Bash(git push:*)
---

# Context

- Current branch: !`git rev-parse --abbrev-ref HEAD`
- Status: !`git status --short`
- Diff stats vs HEAD: !`git diff --stat`
- Working tree diff: !`git diff`
- Recent commits: !`git log --oneline -10`
- Commits ahead of main: !`git log --oneline main..HEAD`
- Commit count ahead of main: !`git rev-list --count main..HEAD`

# Task

Merge the current branch into `main` and delete the branch.

## Rules

- The current branch must have no pending files to commit. If there are pending changes (status above is not empty), stop and ask.
- If the current branch has more than 10 commits ahead of `main`, stop and ask.
- If the current branch is already `main`, stop and inform the user — there is nothing to merge.
- Do not use `--no-verify`.
- Do not force push.
- Do not delete `main` under any circumstance.

## Flow

1. Show a summary of the current branch: name, commit count ahead of main, and the list of commits/changes to be merged.
2. If the branch is clean and has 10 or fewer commits ahead of main, continue. Otherwise, stop and ask.
3. Switch to `main` and pull the latest changes.
4. Merge the feature branch into `main` with fast-forward if possible (`git merge --ff-only` first; if that fails, fall back to a regular merge and inform the user).
5. Push `main` to the remote.
6. After a successful merge and push, delete the feature branch locally (`git branch -d <branch>`). If the branch also exists on the remote, delete it there as well (`git push origin --delete <branch>`).
7. When finished, summarize the merge (commits brought in, fast-forward or merge commit) and the branch deletion that was performed (local and/or remote).