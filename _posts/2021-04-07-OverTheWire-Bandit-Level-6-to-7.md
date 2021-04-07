---
layout: post
date:   2021-04-07 19:21:00 +0100
categories: OverTheWire Bandit
---
#  On the last episode of Bandit..

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
The password for the next level is stored **somewhere on the server** and has all of the following properties:

-   owned by user bandit7
-   owned by group bandit6
-   33 bytes in size

## Commands you may need to solve this level

ls, cd, cat, file, du, find, grep
```

## Lets take a look
```bash
bandit6@bandit:~$ ls
# No result.. Wot?
```

## Mkay, hidden files?
```bash
bandit6@bandit:~$ ls -a
.  ..  .bash_logout  .bashrc  .profile
#Nope - Okay, what?
```

## Lets CD back a bit and look at files, with hidden things shown just to be sure.
```bash
bandit6@bandit:~$ cd ..
bandit6@bandit:/home$ ls -a
.         bandit11  bandit16  bandit20  bandit25      bandit28-git  bandit30-git  bandit4  bandit9
..        bandit12  bandit17  bandit21  bandit26      bandit29      bandit31      bandit5
bandit0   bandit13  bandit18  bandit22  bandit27      bandit29-git  bandit31-git  bandit6
bandit1   bandit14  bandit19  bandit23  bandit27-git  bandit3       bandit32      bandit7
bandit10  bandit15  bandit2   bandit24  bandit28      bandit30      bandit33      bandit8
# Lots of interesting things here, but once again am not going to iterate through everything.
```

## Lets do some more digging with the find command.
```bash
#I don't feel like iterating through every single file on the box, so lets start wit with owners and groups

#/ Is roooot
bandit6@bandit:~$ find / -group bandit6 -user bandit7 -size 33c
...snip...
/var/lib/dpkg/info/bandit7.password
...snip...
```

## What next?
```
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```


## The password for level 7:

HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs


## Connect to level 7.
```bash
bandit6@bandit:~$ ssh bandit7@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
