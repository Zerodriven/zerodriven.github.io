---
layout: post
date:   2021-04-07 23:25:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
The password for the next level can be retrieved by submitting the password of the current level to **port 30000 on localhost**.

## Commands you may need to solve this level

ssh, telnet, nc, openssl, s\_client, nmap
```

## Following the instructions of the previous challenge..
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
redacted
```


## Telnet time!

```bash
bandit14@bandit:~$ telnet localhost 30000
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
redacted
```

## The password for level 15:

redacted

On the next episode of Bandit...
