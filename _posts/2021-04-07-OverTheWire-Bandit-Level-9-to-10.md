---
layout: post
date:   2021-04-07 22:21:00 +0100
categories: OverTheWire Bandit
---
# Level goal
```bash
The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

## Lets take a look and cat the file
```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ cat data.txt
...snip...
#giant object here... Okay, need to look for stuff within it
```

## Lets see what 'strings' does

```bash
...snip...
bandit9@bandit:~$ strings data.txt
WB|{
GhG$
========== the*2i"4
DUJmU
ux.j
=:G e
OxYF
68}j
Q~a`%
========== password
#|-l
G}`:
<I=zsGi
&15h
!G[\
uOZ\K
BYD1
D2?
Z)========== is
x[U*
m/;7
r%z$c
C !n
&/Lhh[}~s
b$J})Q
z3p)
fRk4Ck
Jq{`
fVHi
Y<_M
88)%
Emlld
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
_Gmz
\Uli,
A5RK
S'$0
<4t",
4cXO
...snip...
```

## Mkay, lets see if we can filter that with some equal signs

```bash
bandit9@bandit:~$ strings data.txt | grep "==="
========== the*2i"4
========== password
Z)========== is
&========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

## The password for level 10:

truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk


## Connect to level 10.
```bash
bandit9@bandit:~$ ssh bandit10@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
