---
description: Group changes into semantic commits and squash them.
argument-hint: [optional context for commit messages]
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git add:*), Bash(git -c commit.gpgsign=false commit:*), Bash(git push:*), Bash(git branch:*), Bash(git rev-parse:*)
---

# Context

- Current status: !`git status --short`
- Diff stats: !`git diff --stat`
- Full diff: !`git diff`
- Recent commits: !`git log --oneline -10`
- Current branch: !`git rev-parse --abbrev-ref HEAD`

# Task

Group all current changes into meaningful semantic commits in the current branch.

Optional context for commit messages: `$ARGUMENTS`

## Rules

- Identify related file groups by intent: feature, fix, refactor, tests, docs, chore, release, or config.
- Create multiple commits when there are independent changes. Do not mix unrelated changes in the same commit.
- If `$ARGUMENTS` is not empty, use it as context to adjust commit messages, but do not force that text if it does not accurately describe the changes.
- Use clear, semantic, concise commit messages that follow the repo's recent style (inferred from the recent commits shown above).
- Before committing, check for sensitive or suspicious files (`.env`, tokens, credentials, keys, secrets). If any appear, stop and ask.
- Include new, modified, and deleted files that belong to each group.
- Use `git -c commit.gpgsign=false commit` to avoid signing commits.
- Do not revert existing changes.
- Do not use `--no-verify`.
- Do not amend commits.
- Do not force push.

## Flow

1. Show the proposed commit plan with the files included in each commit.
2. If the grouping is clear, continue. If there is real ambiguity, ask before committing.
3. For each group:
   - Add only the files for that group with `git add <files>`.
   - Create the commit with a semantic message using `git -c commit.gpgsign=false commit -m "..."`.
4. Once all commits have been created, run `git push`.
5. When finished, summarize the commits created and the branch that was pushed.
6. If during the process you created any temporary branch, delete it after pushing.