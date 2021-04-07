---
layout: post
date:   2021-04-07 15:21:00 +0100
categories: OverTheWire Bandit
---
#  On the last episode of Bandit..

```bash
bandit1@bandit:~$ ssh bandit2@localhost
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
## Level Goal

The password for the next level is stored in a file called *spaces in this filename* located in the home directory

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## Lets look at all the files

```bash
bandit2@bandit:~$ ls
spaces in this filename
```

## Lets try to cat the file

```bash
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```

## Lets wrap it in quotes, spaces are bad.

```bash
bandit2@bandit:~$ cat "spaces in this filename"
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

## The password for level 3:

UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

## Connect to level 3.
```bash
bandit2@bandit:~$ ssh bandit3@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...