---
layout: post
date:   2021-04-07 23:24:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
The password for the next level is stored in **/etc/bandit\_pass/bandit14 and can only be read by user bandit14**. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. **Note:** **localhost** is a hostname that refers to the machine you are working on

## Commands you may need to solve this level

ssh, telnet, nc, openssl, s\_client, nmap
```

## Lets take a look and cat the file
```bash
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ cat sshkey.private
-----BEGIN RSA PRIVATE KEY-----
...snip...
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
-----END RSA PRIVATE KEY-----
...snip...
```


## The password for level 14.. Isn't a password.

## Connect to level 14.
```bash
bandit13@bandit:~$ ssh bandit14@localhost -i sshkey.private
```

On the next episode of Bandit...
