---
description: Create a new feature branch using git worktree
---

// turbo-all

1. Pull latest develop
```bash
git -C d:\project\degipa-mock-develop pull origin develop
```

2. Create worktree for the feature (replace `issue-<number>` with actual issue number)
```bash
git worktree add ../degipa-mock-feat-issue-<number> -b feat/issue-<number> develop
```

3. Verify
```bash
git worktree list
```

## Notes

- メインディレクトリ (`degipa-mock`) は常に `main` に留める
- 1 worktree = 1 ブランチ = 1 目的
- 完了後は Draft PR → `git worktree remove ../degipa-mock-feat-issue-<number>`
