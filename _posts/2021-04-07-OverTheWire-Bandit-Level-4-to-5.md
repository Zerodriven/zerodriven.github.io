--
layout: post
date:   2021-04-07 17:21:00 +0100
categories: OverTheWire Bandit
---
#  On the last episode of Bandit..

```bash
bandit3@bandit:~$ ssh bandit4@localhost
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
## Level Goal

The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

# Lets list all the files here..
```bash
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

# Lets look at permissions and files sizes..
```bash
bandit4@bandit:~/inhere$ ls -l
total 40
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file00
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file01
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file02
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file03
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file04
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file05
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file06
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file07
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file08
-rw-r----- 1 bandit5 bandit4 33 May  7  2020 -file09
#Well, that's no help.
```

# Lets look at the 'file' syntax options.
http://www.linfo.org/wildcard.html -- Oooh, wildcards.

```bash
bandit4@bandit:~/inhere$ file *
file: Cannot open `ile00' (No such file or directory).
file: Cannot open `ile01' (No such file or directory).
file: Cannot open `ile02' (No such file or directory).
file: Cannot open `ile03' (No such file or directory).
file: Cannot open `ile04' (No such file or directory).
file: Cannot open `ile05' (No such file or directory).
file: Cannot open `ile06' (No such file or directory).
file: Cannot open `ile07' (No such file or directory).
file: Cannot open `ile08' (No such file or directory).
file: Cannot open `ile09' (No such file or directory).
#Well, that's annoying. Oh yeah the files are all obnoxious.
```

```bash
#Lets try that again..
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

# Lets look at the only ASCII file..
```bash
bandit4@bandit:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

## The password for level 5:

koReBOKuIDDepwhWk7jZC0RTdopnAYKh

## Connect to level 5.
```bash
bandit4@bandit:~$ ssh bandit5@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
