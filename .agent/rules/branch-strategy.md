# Branch Strategy

## Branch Flow

```
feature/xxx ──→ develop ──→ main
fix/xxx     ──→ develop ──→ main
docs/xxx    ──→ develop ──→ main
```

## Branch Definitions

| Branch | Purpose | Merge target | Protection |
| --- | --- | --- | --- |
| `main` | Production-ready code | — | No direct push |
| `develop` | Integration branch | `main` | Via PR |
| `feature/*` | New features | `develop` | Via PR or merge |
| `fix/*` | Bug fixes | `develop` | Via PR or merge |
| `docs/*` | Documentation only | `develop` | Via PR or merge |
| `experiment/*` | Throwaway experiments | `develop` (if successful) | Optional |

## Rules

1. **Never commit directly to `main`** — always go through `develop`
2. **Create working branches from `develop`** — not from `main`
3. **Keep branches short-lived** — merge or delete within a few days
4. **Use descriptive branch names** — `feature/onboarding-flow`, not `feature/stuff`

## Naming Convention

```
<type>/<short-description>

Types: feature, fix, docs, experiment, refactor
```

## Quick Reference

```bash
# Start new feature
git checkout develop
git pull origin develop
git checkout -b feature/my-feature

# Merge to develop
git checkout develop
git pull origin develop
git merge feature/my-feature
git push origin develop

# Release to main
git checkout main
git merge develop
git tag -a v0.1.0 -m "Release v0.1.0"
git push origin main --tags
```
