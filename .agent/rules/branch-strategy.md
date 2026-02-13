# Branch Strategy

## Branch Flow

```
feat/issue-<N> ──→ develop ──→ main
fix/issue-<N>  ──→ develop ──→ main
docs/xxx       ──→ develop ──→ main
```

## Git Worktree 運用

メインディレクトリ (`degipa-mock`) は **常に `main`** に留める。

| ディレクトリ | ブランチ | 用途 |
| --- | --- | --- |
| `degipa-mock` | `main` | 本体。直接コミットしない |
| `degipa-mock-develop` | `develop` | 統合ブランチ（worktree） |
| `degipa-mock-feat-issue-<N>` | `feat/issue-<N>` | 機能開発（worktree） |

```bash
# worktree 作成
git worktree add ../degipa-mock-feat-issue-<N> -b feat/issue-<N> develop

# 作業完了後
git worktree remove ../degipa-mock-feat-issue-<N>
```

## Branch Definitions

| Branch | Purpose | Merge target | Protection |
| --- | --- | --- | --- |
| `main` | Production-ready | — | No direct push |
| `develop` | Integration | `main` | Via PR |
| `feat/*` | New features | `develop` | Via PR or merge |
| `fix/*` | Bug fixes | `develop` | Via PR or merge |
| `docs/*` | Documentation | `develop` | Via PR or merge |

## Rules

1. **Never commit directly to `main`** — always go through `develop`
2. **Create working branches from `develop`** via `git worktree add`
3. **Keep branches short-lived** — merge or delete within a few days
4. **Use issue-based branch names** — `feat/issue-42`, not `feature/stuff`
5. **1 worktree = 1 ブランチ = 1 目的**

## Naming Convention

```
<type>/issue-<number>

Types: feat, fix, docs, experiment, refactor
```
