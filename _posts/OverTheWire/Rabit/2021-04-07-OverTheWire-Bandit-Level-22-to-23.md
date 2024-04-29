---
layout: post
date:   2021-04-09 10:19:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
A program is running automatically at regular intervals from **cron**, 
the time-based job scheduler. 

Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** Looking at shell scripts written by other people is a very useful skill.

The script for this level is intentionally made easy to read. If you are having problems understanding what it does, 
try executing it to see the debug information it prints.

## Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)
```

## Lets go into the directory and look around
```bash
bandit22@bandit:~$ cd /etc/cron.d/
bandit22@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
```

## Back here again, lets cat the file..

```bash
bandit22@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

## Looks like we need to look in user/bin

```bash
bandit22@bandit:/etc/cron.d$ cd /usr/bin/
bandit22@bandit:/usr/bin$ ls -l | grep cron
-rwx------ 1 root     root         142 May 14  2020 cronjob_bandit15_root.sh
-rwx------ 1 root     root         443 Jul 11  2020 cronjob_bandit17_root.sh
-rwxr-x--- 1 bandit22 bandit21     130 May  7  2020 cronjob_bandit22.sh
-rwxr-x--- 1 bandit23 bandit22     211 May  7  2020 cronjob_bandit23.sh
-rwxr-x--- 1 bandit24 bandit23     376 May 14  2020 cronjob_bandit24.sh
-rwx------ 1 root     root         498 May 14  2020 cronjob_bandit25_root.sh
-rwx------ 1 root     root         378 May 14  2020 cronjob_bandit25_root.sh~
-rwx------ 1 root     root         378 May 14  2020 cronjob_bandit25_root.sz~
-rwxr-xr-x 1 root     crontab    40264 Oct  7  2017 crontab
```

## Lets run and then look in the bandit23 file

```bash
bandit22@bandit:/usr/bin$ cronjob_bandit23.sh
Copying passwordfile /etc/bandit_pass/bandit22 to /tmp/8169b67bd894ddbb4412f91573b38db3
bandit22@bandit:/usr/bin$ cat cronjob_bandit23.sh
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

## Okay, so the mytarget variable is probably the key here, what if we run this manually?

```bash
bandit22@bandit:/usr/bin$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
```

## Okay, so it has been run and according to the script it moves it to the tmp/filename

```bash
bandit22@bandit:/usr/bin$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
redacted
```
VICTORY.

## The password for level 23: 	

redacted

On the next episode of Bandit...

```bash
ssh bandit23@localhost
redacted
```