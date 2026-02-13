---
description: Merge a feature worktree branch into develop
---

1. Ensure all changes are committed in the feature worktree

// turbo
2. Switch to develop worktree and pull latest
```bash
git -C d:\project\degipa-mock-develop pull origin develop
```

3. Merge the feature branch (replace `feat/issue-<number>`)
```bash
git -C d:\project\degipa-mock-develop merge feat/issue-<number>
```

4. Resolve conflicts if any, then push
// turbo
```bash
git -C d:\project\degipa-mock-develop push origin develop
```

5. Remove the feature worktree and delete the branch
```bash
git worktree remove ../degipa-mock-feat-issue-<number>
git branch -d feat/issue-<number>
```
