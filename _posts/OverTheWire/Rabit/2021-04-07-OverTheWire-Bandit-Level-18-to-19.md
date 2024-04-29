---
layout: post
date:   2021-04-08 23:28:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.
```

## This one caused me sadness, after some digging..
```bash

bandit17@bandit:/home/bandit18$ ssh -t bandit18@localhost cat readme
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit17/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/home/bandit17/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/home/bandit17/.ssh/id_rsa": bad permissions
bandit18@localhost's password:
redacted
Connection to localhost closed.
```

```bash
bandit17@bandit:/home/bandit18$ man ssh
 -t      Force pseudo-terminal allocation.  This can be used to execute arbitrary screen-based programs on a
             remote machine, which can be very useful, e.g. when implementing menu services.  Multiple -t options
             force tty allocation, even if ssh has no local tty.
```

VICTORY.

## The password for level 18: 	

redacted

On the next episode of Bandit...

```bash
ssh bandit18@localhost
redacted
```