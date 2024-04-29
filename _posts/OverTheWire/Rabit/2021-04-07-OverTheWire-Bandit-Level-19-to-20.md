---
layout: post
date:   2021-04-08 23:29:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit\_pass), after you have used the setuid binary.
```

## Lets follow some instructions
```bash
bandit19@bandit:~$ ls
bandit20-do
bandit19@bandit:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```

## Lets check something and then run the command

```bash
bandit19@bandit:~$ id
uid=11019(bandit19) gid=11019(bandit19) groups=11019(bandit19)
bandit19@bandit:~$ ./bandit20-do id
uid=11019(bandit19) gid=11019(bandit19) euid=11020(bandit20) groups=11019(bandit19)
# That's interesting.
```

## Okay, it says the password location in the level info..

```bash
bandit19@bandit:~$ ./bandit20-do ls /etc/bandit_pass/bandit20
/etc/bandit_pass/bandit20
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
redacted
```

VICTORY.

## The password for level 20: 	

redacted

On the next episode of Bandit...

```bash
ssh bandit20@localhost
redacted
```