---
description: "Merge current branch into main and delete the branch."
---

Merge current branch into main and delete the branch.

Rules:

- First inspect the full repository state:
  - `git status --short`
  - `git diff --stat`
  - `git diff`
  - `git log --oneline -10`
- Check if the current branch has no pending files to commit. If there are pending changes, stop and ask.
- If the current branch has more than 10 commits, stop and ask.

Flow:

1. Show the summary of the current branch commits and changes.
2. If the branch is clean and has 10 or fewer commits, continue. If there are pending changes or more than 10 commits, stop and ask.
3. Merge the current branch into main with fast-forward if possible.
4. After a successful merge, delete the current branch.
5. When finished, summarize the merge and branch deletion that was performed.