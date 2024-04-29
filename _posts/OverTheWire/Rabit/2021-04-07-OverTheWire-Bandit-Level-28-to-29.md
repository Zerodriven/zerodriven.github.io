---
layout: post
date:   2021-04-09 11:22:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There is a git repository at `ssh://bandit28-git@localhost/home/bandit28-git/repo`. The password for the user `bandit28-git` is the same as for the user `bandit28`.

Clone the repository and find the password for the next level.
```

## Back to regularly scheduled linuxing - Firstly, lets pull the repo into a tmp dir.

```bash
bandit28@bandit:/tmp/zd28/repo$ mkdir /tmp/zd28
bandit28@bandit:/tmp/zd28/repo$ cd /tmp/zd28
bandit28@bandit:/tmp/zd28/repo$ git clone ssh://bandit28-git@localhost/home/bandit28-git/repo
bandit28@bandit:/tmp/zd28/repo2$ cd repo
bandit28@bandit:/tmp/zd28/repo2/repo$ cat README.md
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

## Mmmmkay, that's helpful. Anything in the log?

```bash
bandit28@bandit:/tmp/zd28/repo2/repo$ git log .
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak

commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data

commit de2ebe2d5fd1598cd547f4d56247e053be3fdc38
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    initial commit of README.md
```

## Oooo we can look at the file history (ref: https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

```bash
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak

diff --git a/README.md b/README.md
index 3f7cee8..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: bbc96594b4e001778eee9975372716b2
+- password: xxxxxxxxxx


commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data

diff --git a/README.md b/README.md
bandit28@bandit:/tmp/zd28/repo2/repo$ clear
bandit28@bandit:/tmp/zd28/repo2/repo$ git log -p
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    fix info leak

diff --git a/README.md b/README.md
index 3f7cee8..5c6457b 100644
--- a/README.md
+++ b/README.md
@@ -4,5 +4,5 @@ Some notes for level29 of bandit.
 ## credentials

 - username: bandit29
-- password: redacted
+- password: xxxxxxxxxx


commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

    add missing data
```

VICTORY

Password is: redacted