---
layout: post
date:   2021-04-09 10:18:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
A program is running automatically at regular intervals from **cron**,
the time-based job scheduler. Look in **/etc/cron.d/** 
for the configuration and see what command is being executed.
```

## Lets look at some directories
```bash
bandit21@bandit:/etc$ cd cron.d
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit
cronjob_bandit15_root  cronjob_bandit22       cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23       cronjob_bandit25_root
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

## Lets run the sh file.

```bash
bandit21@bandit:/etc/cron.d$ cd /usr/bin/
bandit21@bandit:/usr/bin$ ./cronjob_bandit22.sh
chmod: changing permissions of '/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv': Operation not permitted
./cronjob_bandit22.sh: line 3: /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv: Permission denied
```

## Lets look in there..
```bash
bandit21@bandit:/usr/bin$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
redacted
```

VICTORY.

## The password for level 22: 	

redacted

On the next episode of Bandit...

```bash
ssh bandit21@localhost
redacted
```