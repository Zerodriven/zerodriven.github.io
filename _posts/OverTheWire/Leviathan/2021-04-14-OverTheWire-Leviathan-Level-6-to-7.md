---
layout: post
date:   2021-04-18 09:10:00 +0100
categories: OverTheWire Leviathan
---


# Leviathan 6
```

Username: leviathan6
Password: UgaoFee4li

Data for the levels can be found in **the homedirectories**. You can look at **/etc/leviathan\_pass** for the various level passwords.
```


## Lets take a look.

```bash
leviathan6@leviathan:~$ ls
leviathan6
```

## ltrace it, seems the norm now

```bin
leviathan6@leviathan:~$ ltrace ./leviathan6
__libc_start_main(0x804853b, 1, 0xffffd784, 0x80485e0 <unfinished ...>
printf("usage: %s <4 digit code>\n", "./leviathan6"usage: ./leviathan6 <4 digit code>
)                      = 35
exit(-1 <no return ...>
+++ exited (status 255) +++
leviathan6@leviathan:~$ ltrace ./leviathan6 0000
__libc_start_main(0x804853b, 2, 0xffffd784, 0x80485e0 <unfinished ...>
atoi(0xffffd8b0, 0, 0xf7e40890, 0x804862b)                                = 0
puts("Wrong"Wrong
)                                                             = 6
+++ exited (status 0) +++
```

## What the hell is atoi?

```bash
https://man7.org/linux/man-pages/man3/atoi.3.html
```

## String to int? Guess we're going to have to write a scipt to loop again.

```bash
leviathan6@leviathan:~$ mkdir /tmp/zdl6
leviathan5@leviathan:~$ cd /tmp/zdl6
leviathan6@leviathan:/tmp/zdl6$ touch beep.sh
leviathan6@leviathan:/tmp/zdl6$ nano beep.sh

#!/bin/bash
for i in {0000..9999}
do
~/leviathan6 $i
done

leviathan6@leviathan:/tmp/zdl6$ chmod 777 beep.sh
```

## Lets run this and see what happens

```bash
leviathan6@leviathan:/tmp/zdl6$ ./beep.sh
...snip...
$ whoami
leviathan7
$ cat /etc/leviathan_pass/leviathan7
ahy7MaeBo9
```

VICTORY.

```
ahy7MaeBo9 
```


