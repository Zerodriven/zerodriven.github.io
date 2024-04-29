---
layout: post
date:   2021-04-09 11:25:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There is a git repository at `ssh://bandit31-git@localhost/home/bandit31-git/repo`. The password for the user `bandit31-git` is the same as for the user `bandit31`.

Clone the repository and find the password for the next level.
```

## Another... Another git one.. Same process... temp dir, clone, inspect.

```bash
bandit31@bandit:~$ mkdir /tmp/zd31
bandit31@bandit:~$ cd /tmp/zd31
bandit31@bandit:/tmp/zd31$ git clone ssh://bandit31-git@localhost/home/bandit31-git/repo
Cloning into 'repo'...
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (4/4), done.
bandit31@bandit:/tmp/zd31$ ls
repo
bandit31@bandit:/tmp/zd31$ cd repo/
bandit31@bandit:/tmp/zd31/repo$ ls
README.md
bandit31@bandit:/tmp/zd31/repo$ cat README.md
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

## So.. I pushed the .txt file and guess what? Nothing happened. I wonder..

```bash
bandit31@bandit:/tmp/zd31/repo$ ls -a
.  ..  .git  .gitignore  key.txt  README.md
```

## Sneaky. Removed the txt from gitignore.

```bash
bandit31@bandit:/tmp/zd31/repo$ ls -a
.  ..  .git  .gitignore  key.txt  README.md
bandit31@bandit:/tmp/zd31/repo$ git add .
bandit31@bandit:/tmp/zd31/repo$ git commit -m "Sneaky"
[master b792eac] Sneaky
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 key.txt
bandit31@bandit:/tmp/zd31/repo$ git push
Could not create directory '/home/bandit31/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit31/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit31-git@localhost's password:
Counting objects: 4, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (4/4), 330 bytes | 0 bytes/s, done.
Total 4 (delta 0), reused 0 (delta 0)
remote: ### Attempting to validate files... ####
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
remote: Well done! Here is the password for the next level:
remote: redacted
remote:
remote: .oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.oOo.
remote:
To ssh://localhost/home/bandit31-git/repo
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'ssh://bandit31-git@localhost/home/bandit31-git/repo'
```

VICTORY and hey, didn't even have to google a thing on this one. Heh.

Password is: redacted