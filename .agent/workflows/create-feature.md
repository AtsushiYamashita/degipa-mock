---
description: Create a new feature branch using git worktree
---

// turbo-all

1. Pull latest develop

```bash
git -C d:\project\degipa-mock-develop pull origin develop
```

2. Create worktree for the feature (replace N and description)

```bash
git worktree add ../degipa-mock-feat-N-description -b feat/N-description develop
```

Example: `git worktree add ../degipa-mock-feat-42-add-user-auth -b feat/42-add-user-auth develop`

3. Verify

```bash
git worktree list
```

## Notes

- メインディレクトリ (`degipa-mock`) は常に `main` に留める
- 1 worktree = 1 ブランチ = 1 目的
- ブランチ名は `<type>/<issue-number>-<short-description>` 形式
- 完了後は Draft PR → 人間がマージ → `git worktree remove`
