---
layout: single
date: 2026-06-22
categories: Git
classes: wide
keywords:
  - Git
---
Scenario:

Unmanageable amount of local git branches and you want to delete all of the local copies. This is specifically for Windows. You can look at all your local git branches with the most basic of git commands:

```bash
git branch
```

![](/assets/20260622075842.png)

As you can see, manageable list right? What happens when it becomes:

![](/assets/20260622080508.png)

Or gets even worse? Or longer? Of if you've got (Because of sheer laziness) hundreds of unmanaged local branches? Ez. Fix is ez. Assuming you do actually want to delete them all as part of a cleanup

1. Open Git Bash
2. CD to relevant directory
```bash
git branch | grep -v BRANCHNAME | xargs git branch -D
```
3. Hit return (This will return a few more details

![](/assets/20260622080337.png)

Then ta-da, all gone:

![](/assets/P20260622080758.png)