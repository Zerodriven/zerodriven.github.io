---
layout: post
date:   2021-04-07 13:21:00 +0100
categories: OverTheWire Bandit
---

During a level of boredom I've not felt in a whille I rediscovered https://overthewire.org/wargames/bandit/ - A website for beginner wargames in Linux, so you know I thought I'd give it a shot. Anything in this series will go through my way of thinking and the way I do things.. But with extra comments. Not pretty but does the job.

Through each of these I use google to find syntax, I also use "man [command]" if I'm being extra curious.

# Connecting to the bandit servers:

## Run the following command in shell:

```bash
# SSH is a required install. 
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

## Level Goal

```bash
## Level Goal

The password for the next level is stored in a file called **readme** located in the home directory.

Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## List out files in the home directory (Where you start when SSHing in)

```bash
#List the folder directory using the 'ls' command
bandit0@bandit:~$ ls
readme
```

## Reading the content of the file
```bash
#less can be used here, but the site says use cat

bandit0@bandit:~$ cat readme
redacted
bandit0@bandit:~$
```

## The password for level 1
redacted

### Connecting to another username on the same server.

```bash
bandit0@bandit:~$ ssh bandit1@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...