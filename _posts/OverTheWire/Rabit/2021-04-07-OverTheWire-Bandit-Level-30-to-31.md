---
layout: post
date:   2021-04-09 11:24:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There is a git repository at `ssh://bandit30-git@localhost/home/bandit30-git/repo`. The password for the user `bandit30-git` is the same as for the user `bandit30`.

Clone the repository and find the password for the next level.
```

## Another git one.. Same process... temp dir, clone, inspect.

```bash
bandit30@bandit:~$ mkdir /tmp/zd30
bandit30@bandit:~$ cd /tmp/zd30
bandit30@bandit:/tmp/zd30$ git clone ssh://bandit30-git@localhost/home/bandit30-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit30/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit30/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit30-git@localhost's password:
remote: Counting objects: 4, done.
Receiving objects: 100% (4/4), 297 bytes | 0 bytes/s, done.
remote: Total 4 (delta 0), reused 0 (delta 0)
bandit30@bandit:/tmp/zd30$ ls
repo
bandit30@bandit:/tmp/zd30$ cd repo/
bandit30@bandit:/tmp/zd30/repo$ ls
README.md
bandit30@bandit:/tmp/zd30/repo$ cat README.md
just an epmty file... muahaha
```

## Awh, that's mean. Will look at branches, history etc now.

```bash
bandit30@bandit:/tmp/zd30/repo$ git branch -r
  origin/HEAD -> origin/master
  origin/master
bandit30@bandit:/tmp/zd30/repo$ git log -p
commit 3aefa229469b7ba1cc08203e5d8fa299354c496b
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:54 2020 +0200

    initial commit of README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..029ba42
--- /dev/null
+++ b/README.md
@@ -0,0 +1 @@
+just an epmty file... muahaha
```

## The branches were no use.. What else can we try. Tags?

```bash
bandit30@bandit:/tmp/zd30/repo$ git tag
secret
```

## Okay, what's inside secret?

```bash
bandit30@bandit:/tmp/zd30/repo$ git show secret
redacted
```


VICTORY

Password is: redacted