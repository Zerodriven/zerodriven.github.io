---
layout: post
date:   2021-04-09 11:23:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There is a git repository at `ssh://bandit29-git@localhost/home/bandit29-git/repo`. The password for the user `bandit29-git` is the same as for the user `bandit29`.

Clone the repository and find the password for the next level.
```

## Hey, the last one said to do this too - Firstly, lets pull the repo into a tmp dir.

```bash
bandit29@bandit:~$ mkdir /tmp/zd29
bandit29@bandit:~$ cd /tmp/zd29
bandit29@bandit:/tmp/zd29$ git clone ssh://bandit29-git@localhost/home/bandit29-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit29/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit29/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit29-git@localhost's password:
remote: Counting objects: 16, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 16 (delta 2), reused 0 (delta 0)
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (2/2), done.
```

## Time to look around

```bash
bandit29@bandit:/tmp/zd29/repo$ ls
README.md
bandit29@bandit:/tmp/zd29/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

## Hey hey hey, production..

```bash
bandit29@bandit:/tmp/zd29/repo$ git branch -r
  origin/HEAD -> origin/master
  origin/dev
  origin/master
  origin/sploits-dev
```

## Look, a wild dev branch appears! I wonder what's inside..

```bash
bandit29@bandit:/tmp/zd29/repo$ git checkout dev
Branch dev set up to track remote branch dev from origin.
Switched to a new branch 'dev'
bandit29@bandit:/tmp/zd29/repo$ ls
code  README.md
bandit29@bandit:/tmp/zd29/repo$ cat README.md
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: 5b90576bedb2cc04c86a9e924ce42faf
```


VICTORY

Password is: 5b90576bedb2cc04c86a9e924ce42faf