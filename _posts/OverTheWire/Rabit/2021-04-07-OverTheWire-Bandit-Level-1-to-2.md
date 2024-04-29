---
layout: post
date:   2021-04-07 14:21:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
## Level Goal

The password for the next level is stored in a file called **\-** located in the home directory

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## Lets look at all the files

```bash
bandit1@bandit:~$ ls
-
```

## Lets try to cat the file

```bash
bandit1@bandit:~$ cat -
#Nothing happens
```

## Lets speciy the folder we're in..

```bash
# A **dot slash** is a **dot** followed immediately by a forward **slash** ( ./ ). It is used in **Linux** and Unix to execute a compiled program in the current directory
bandit1@bandit:~$ cat ./-
redacted 
```

## The password for level 2:

redacted

## Connect to level 2.
```bash
bandit1@bandit:~$ ssh bandit2@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...