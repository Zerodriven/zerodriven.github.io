---
layout: post
date:   2021-04-07 23:21:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

## Lets take a look and cat the file
```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
bandit10@bandit:~$
#Base64.. There's probably a way to read that.
```

## Lets do some basing
```bash
bandit10@bandit:~$ man base64
...snip...
SYNOPSIS
       base64 [OPTION]... [FILE]
	   -d, --decode
...snip...
```

```bash
bandit10@bandit:~$ base64 -d data.txt
The password is redacted
```

## The password for level 10:

redacted

## Connect to level 10.
```bash
bandit10@bandit:~$ ssh bandit11@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
