---
description: Create a new feature branch from develop
---

// turbo-all

1. Switch to develop and pull latest
```bash
git checkout develop
git pull origin develop
```

2. Create the new branch (replace `feature/xxx` with your branch name)
```bash
git checkout -b feature/xxx
```

3. Verify
```bash
git branch --show-current
```
