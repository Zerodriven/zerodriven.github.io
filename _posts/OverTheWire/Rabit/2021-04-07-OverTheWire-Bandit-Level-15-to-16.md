---
layout: post
date:   2021-04-07 23:26:00 +0100
categories: OverTheWire Bandit
---

# Level goal
```bash
The password for the next level can be retrieved by submitting the password of the current level to **port 30001 on localhost** using SSL encryption.

**Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign\_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…**

## Commands you may need to solve this level

ssh, telnet, nc, openssl, s\_client, nmap
```

## So.. Telnet isn't the answer here. The level goal mentions ssl, there's a tool called openssl - Lets look there.
```bash
bandit14@bandit:~$ man openssl
openssl command [ command_opts ] [ command_args ]
s_client
           This implements a generic SSL/TLS client which can establish a transparent connection to a remote server
           speaking SSL/TLS. It's intended for testing purposes only and provides only rudimentary interface
           functionality but internally uses mostly all functionality of the OpenSSL ssl library.
```


## Lets see what openssl and s_client does

```bash
bandit15@bandit:~$ openssl s_client -connect localhost:30001
CONNECTED(00000003)
depth=0 CN = localhost
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = localhost
verify return:1
---
Certificate chain
 0 s:/CN=localhost
   i:/CN=localhost
---
...snip...

    Start Time: 1617822989
    Timeout   : 7200 (sec)
    Verify return code: 18 (self signed certificate)
    Extended master secret: yes
---
...snip...
BfMYroe26WYalil77FoDi9qh59eK5xNr
Correct!
redacted

closed
```

## The password for level 16:

redacted

On the next episode of Bandit...

```bash
ssh bandit16@localhost
redacted
```