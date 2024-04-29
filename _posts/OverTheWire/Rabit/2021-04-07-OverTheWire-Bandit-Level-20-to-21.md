---
layout: post
date:   2021-04-08 23:30:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

## Commands you may need to solve this level

ssh, nc, cat, bash, screen, tmux, Unix ‘job control’ (bg, fg, jobs, &, CTRL-Z, …)
```

## This sounds complex. Lets see what it does.
```bash
bandit20@bandit:~$ ls
suconnect
bandit20@bandit:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```

## Guessing some sort of server is needed here. NC is netcat right? Have to open 2 terminals..

```bash
bandit20@bandit:~$ echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -lp 8080
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
# It wasn't letting me post/connect using nc -lp 8080
# had to google it to find this: https://unix.stackexchange.com/questions/289364/netcat-doesnt-print-response
```

```bash
bandit20@bandit:~$ ./suconnect 8080
Read: redacted
Password matches, sending next password
```


VICTORY.

## The password for level 21: 	

redacted
On the next episode of Bandit...

```bash
ssh bandit21@localhost
redacted
```