---
layout: post
date:   2021-04-17 10:52:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 4
```

Username: leviathan4
Password: vuH0coox6m

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look.

```bash
leviathan4@leviathan:~$ ls
leviathan4@leviathan:~$ ls -la
total 24
drwxr-xr-x  3 root root       4096 Aug 26  2019 .
drwxr-xr-x 10 root root       4096 Aug 26  2019 ..
-rw-r--r--  1 root root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root root       3526 May 15  2017 .bashrc
-rw-r--r--  1 root root        675 May 15  2017 .profile
dr-xr-x---  2 root leviathan4 4096 Aug 26  2019 .trash
leviathan4@leviathan:~$ cd .trash
leviathan4@leviathan:~/.trash$
```

## I like trash. What's inside?

```bin
leviathan4@leviathan:~/.trash$ ls
bin
leviathan4@leviathan:~/.trash$ ./bin
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010
```

## I'm not going to find a command for that. So..

1. https://www.rapidtables.com/convert/number/binary-to-string.html
2. Paste in the binary code
3. Victory

```bash
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010
Tith4cokei
```

VICTORY.

```
Tith4cokei 
```
