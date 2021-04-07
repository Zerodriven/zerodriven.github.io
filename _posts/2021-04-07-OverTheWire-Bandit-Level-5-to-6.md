---
layout: post
date:   2021-04-07 18:21:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

-   human-readable
-   1033 bytes in size
-   not executable

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## As always, lets see what's listed

```bash
bandit5@bandit:~$ ls
inhere
```

## Lets go in there and list everything
```bash
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
bandit5@bandit:~/inhere$
```

## Lets look at the file info
```bash
bandit5@bandit:~/inhere$ file *
maybehere00: directory
maybehere01: directory
maybehere02: directory
maybehere03: directory
maybehere04: directory
maybehere05: directory
maybehere06: directory
maybehere07: directory
maybehere08: directory
maybehere09: directory
maybehere10: directory
maybehere11: directory
maybehere12: directory
maybehere13: directory
maybehere14: directory
maybehere15: directory
maybehere16: directory
maybehere17: directory
maybehere18: directory
maybehere19: directory
#Dammit. Directories. I'm not manually iterating through all these.

```

## Lets look at file size syntax and see if there's a way to find all files in the inhere directory with a 1033 byte size.

```bash
bandit5@bandit:~/inhere$ man find
...snip...
 -size n[cwbkMG]
              `c'    for bytes
...snip...
```

## Lets see how this works.. 
```bash
bandit5@bandit:~/inhere$ find -size 1033c
./maybehere07/.file2
# Thats's interesting. What's in here?
```

## Lets look in the file

```bash
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
DXjZPULLxYr17uwoI01bNLQbtFemEgo7








                                        bandit5@bandit:~/inhere$
# ALL THE WHITESPACE to make it 1033 bytes.
```


## The password for level 6:

DXjZPULLxYr17uwoI01bNLQbtFemEgo7

## Connect to level 6.
```bash
bandit5@bandit:~$ ssh bandit6@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
