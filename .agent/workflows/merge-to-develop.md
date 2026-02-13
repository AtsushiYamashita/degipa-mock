---
description: Merge a feature branch into develop
---

1. Ensure all changes are committed on your feature branch

// turbo
2. Switch to develop and pull latest
```bash
git checkout develop; git pull origin develop
```

3. Merge the feature branch (replace `feature/xxx`)
```bash
git merge feature/xxx
```

4. Resolve conflicts if any, then:
// turbo
```bash
git push origin develop
```

5. Delete the feature branch (optional)
```bash
git branch -d feature/xxx
```
