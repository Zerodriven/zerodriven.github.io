---
layout: post
date:   2021-04-07 17:21:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
## Level Goal

The password for the next level is stored in a hidden file in the **inhere** directory.

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## Lets look at all the files

```bash
bandit3@bandit:~$ ls
inhere
```

## Lets go into the directory

```bash
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$
# cd: change current working directory - Universal. 
```

## Lets look in here

```bash
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$
#Oh yeah, they're hidden! Lets show all the things.
bandit3@bandit:~/inhere$ ls -a
#  ls -a: list all files including hidden file starting with '.'
.  ..  .hidden
```

## Lets look in the hidden file
```bash
bandit3@bandit:~/inhere$ cat .hidden
redacted
```

## The password for level 4:

redacted

## Connect to level 4.
```bash
bandit3@bandit:~$ ssh bandit4@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...