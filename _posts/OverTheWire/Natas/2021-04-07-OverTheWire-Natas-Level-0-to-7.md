---
layout: post
date:   2021-04-10 10:10:00 +0100
categories: OverTheWire Natas
---


# Natas - What is it?
```
# Natas

Natas teaches the basics of serverside web-security.

Each level of natas consists of its own website located at **http://natasX.natas.labs.overthewire.org**, where X is the level number. There is **no SSH login**. To access a level, enter the username for that level (e.g. natas0 for level 0) and its password.

Each level has access to the password of the next level. Your job is to somehow obtain that next password and level up. **All passwords are also stored in /etc/natas\_webpass/**. E.g. the password for natas5 is stored in the file /etc/natas\_webpass/natas5 and only readable by natas4 and natas5.

Start here:


Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

## I'll be using FireFox and probably Burpsuite for these.

# Level 0
```bash
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

## First step, look at the source

VICTORY.


gtVrDuiDfck831PqWsLEZy5gyDz1clto 

# Level 1

```
Username: natas1
URL:      http://natas1.natas.labs.overthewire.org
```


## As last time, developer tools


VICTORY.

ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi 

# Level 2

```
Username: natas2
URL:      http://natas2.natas.labs.overthewire.org
```

## Dev tools again.


## Files? Those sound good.


## Users sound even better.


VICTORY

sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

# Level 3
```
Username: natas3
URL:      http://natas3.natas.labs.overthewire.org
```

## You can assume I've looked at the webpage.. Straight to dev tools

## Ah robots, my old WordPress enemy.


VICTORY

	Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ

# Level 4
```
Username: natas4
URL:      http://natas4.natas.labs.overthewire.org
```


## Lets send that to the repeater and look at what we send


## Lets add some referers..

VICTORY

iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

# Level 5


## Not logged in? Well, the answer is yummy. Sent the request to Burp's repeater..


## What's this? Logged in boolean? Lets change and send.

VICTORY

The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1

# Level 6


VICTORY

Access granted. The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9

# Level 7



## Traversal for the win! I remember things!


VICTORY

DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
