---
layout: post
date:   2021-04-08 23:27:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There are 2 files in the homedirectory: **passwords.old and passwords.new**. The password for the next level is in **passwords.new** and is the only line that has been changed between **passwords.old and passwords.new**

**NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19**
```

## Lets diff. Didn't even need to man this.
```bash
bandit17@bandit:~$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> redacted
```

## Lets try to connect!
```bash
bandit17@bandit:~$ ssh bandit18@localhost
...snip...
Byebye !
Connection to localhost closed.
```

## What? Oh, should really read the goal.. On to the next one?

VICTORY.

## The password for level 18: 	

redacted

On the next episode of Bandit...

```bash
ssh bandit18@localhost
redacted
```