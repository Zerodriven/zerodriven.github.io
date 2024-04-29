---
layout: post
date:   2021-04-17 10:51:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 3
```

Username: leviathan3
Password: redacted

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look.

```bash
leviathan3@leviathan:~$ ls
level3
leviathan3@leviathan:~$ ./level3
Enter the password> qwerty
bzzzzzzzzap. WRONG
leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x8048618, 1, 0xffffd794, 0x80486d0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                = -1
printf("Enter the password> ")                                            = 20
fgets(Enter the password> kakaka
"kakaka\n", 256, 0xf7fc55a0)                                        = 0xffffd5a0
strcmp("kakaka\n", "snlprintf\n")                                         = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                                                = 19
+++ exited (status 0) +++
```

## Sweet. Free password. Round 2

```bash
leviathan3@leviathan:~$ ltrace ./level3
__libc_start_main(0x8048618, 1, 0xffffd794, 0x80486d0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                     = -1
printf("Enter the password> ")                                                 = 20
fgets(Enter the password> snlprintf
"snlprintf\n", 256, 0xf7fc55a0)                                          = 0xffffd5a0
strcmp("snlprintf\n", "snlprintf\n")                                           = 0
puts("[You've got shell]!"[You've got shell]!
)                                                    = 20
geteuid()                                                                      = 12003
geteuid()                                                                      = 12003
setreuid(12003, 12003)                                                         = 0
system("/bin/sh"$
```

## Much easier than #3 - But lets clear it up.

```bash
leviathan3@leviathan:~$ ./level3
Enter the password> kakaka
bzzzzzzzzap. WRONG
leviathan3@leviathan:~$ ./level3
Enter the password> snlprintf
[You've got shell]!
$ whoami
leviathan4
$ cat /etc/leviathan_pass/leviathan4
redacted
```

VICTORY.

```
redacted 
```
