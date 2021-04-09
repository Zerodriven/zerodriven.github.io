---
layout: post
date:   2021-04-07 23:22:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
...snip...
Rot13 on Wikipedia
...snip...
```

## Lets take a look and cat the file
```bash
bandit11@bandit:~$ ls
data.txt
bandit11@bandit:~$ cat data.txt
Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
#They weren't kidding. Let's l;
```

## What even is Rot13
```shell
**ROT13** ("**rotate by 13 places**", sometimes hyphenated **ROT-13**) is a simple letter [substitution cipher](https://en.wikipedia.org/wiki/Substitution_cipher "Substitution cipher") that replaces a letter with the 13th letter after it in the alphabet. ROT13 is a special case of the [Caesar cipher](https://en.wikipedia.org/wiki/Caesar_cipher "Caesar cipher") which was developed in ancient Rome.
```

## So, I can't install tools on the box so lets go to a rot13 decryptor.. https://rot13.com/ and decrypt the rotated key from above..

```text
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

## The password for level 12:

5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

## Connect to level 12.
```bash
bandit11@bandit:~$ ssh bandit12@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
