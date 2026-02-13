# Branch Strategy

## Branch Flow

```text
feat/N-description ──→ develop ──→ main
fix/N-description  ──→ develop ──→ main
docs/N-description ──→ develop ──→ main
```

## Naming Convention

```text
<type>/<issue-number>-<short-description>

Types: feat, fix, docs, experiment, refactor
```

**Examples:**

```text
feat/42-add-user-auth
fix/15-login-error
docs/7-user-flow-spec
refactor/23-extract-pure-functions
```

**Rules:**
- 番号が先（ソートしやすい）、説明が後（内容がわかる）
- 説明は 3-5 words、kebab-case
- `feat/issue-42` のような **説明なしの命名は禁止**

## Git Worktree 運用

メインディレクトリ (`degipa-mock`) は **常に `main`** に留める。

| ディレクトリ | ブランチ | 用途 |
| --- | --- | --- |
| `degipa-mock` | `main` | 本体。直接コミットしない |
| `degipa-mock-develop` | `develop` | 統合ブランチ（worktree） |
| `degipa-mock-feat-N-desc` | `feat/N-desc` | 機能開発（worktree） |

```bash
# worktree 作成（例: Issue #42 のユーザー認証）
git worktree add ../degipa-mock-feat-42-add-user-auth -b feat/42-add-user-auth develop

# 作業完了後
git worktree remove ../degipa-mock-feat-42-add-user-auth
```

## Branch Definitions

| Branch | Purpose | Merge target | Protection |
| --- | --- | --- | --- |
| `main` | Production-ready | — | No direct push, pre-commit hook |
| `develop` | Integration | `main` | Via PR |
| `feat/*` | New features | `develop` | Via PR or merge |
| `fix/*` | Bug fixes | `develop` | Via PR or merge |
| `docs/*` | Documentation | `develop` | Via PR or merge |

## Rules

1. **Never commit directly to `main`** — pre-commit hook が強制
2. **Create working branches from `develop`** via `git worktree add`
3. **Keep branches short-lived** — merge or delete within a few days
4. **1 worktree = 1 ブランチ = 1 目的**
5. **ブランチ名から何をしているかわかること**

## Anti-Patterns

- ❌ PR 済みブランチを使い回して別の変更を積む
- ❌ マージ後のブランチを削除しない
- ❌ develop に直接コミット（feature ブランチを経由する）
- ❌ `gh pr merge` / `gh pr ready` をエージェントが実行する
- ❌ 説明のないブランチ名（`feat/issue-42`）
- ❌ 巨大な 1 コミット（目安: 100 行 / 3 ファイル以内）

## AI-Human Collaboration

- AI は常に **Draft PR** を作成する（Ready にするのは人間）
- マージは **人間が GitHub UI で行う**（`gh pr merge` 禁止）
- AI のコミットは Antigravity が自動で author 設定するため追加対応不要
- AI が作成した PR は、ジュニア開発者のコードと同じレベルでレビューする
