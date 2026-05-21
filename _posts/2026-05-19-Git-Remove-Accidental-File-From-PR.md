---
layout: single
date:   2026-05-19 08:34
categories: git
---
Scenario: Wrote code, did a PR, got comments and fixed them. Accidentally started work on a different piece of work but committed change to the same codebase as the previous PR

Fix:

1. Open cmd
2. Go to project directory

```powershell
cd path\to\project
```

```powershell
git checkout HEAD~1 \Path\To\File\File.cs
```

This reverts the file back to the last known copy before your changes were published.