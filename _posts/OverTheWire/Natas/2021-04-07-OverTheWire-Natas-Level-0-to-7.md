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

### 'll be using FireFox and probably Burpsuite for these.

# Level 0
```bash
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

### First step, look at the source

![](/assets/1.png)
![](/assets/2.png)

VICTORY.

```
gtVrDuiDfck831PqWsLEZy5gyDz1clto 
```

# Level 1

```
Username: natas1
URL:      http://natas1.natas.labs.overthewire.org
```


### As last time, developer tools
![](/assets/3.png)

VICTORY.
```
ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi 
```

# Level 2

```
Username: natas2
URL:      http://natas2.natas.labs.overthewire.org
```

### Dev tools again.
![](/assets/4.png)

### Files? Those sound good.
![](/assets/5.png)

### Users sound even better.
![](/assets/6.png)

VICTORY

```
sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
```

# Level 3
```
Username: natas3
URL:      http://natas3.natas.labs.overthewire.org
```

### Ah robots, my old enemy.
![](/assets/7.png)

### Secrets? WHAT SECRETS
![](/assets/8.png)

### EVEN MORE SECRETS

![](/assets/9.png)

### Can I haz sekret now plz?
![](/assets/10.png)

VICTORY
```
	Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```

# Level 4
```
Username: natas4
URL:      http://natas4.natas.labs.overthewire.org
```

![](/assets/11.png)

### Lets send that to the repeater...

![](/assets/12.png)

### Lets add some referers..

![](/assets/13.png)

![](/assets/14.png)

VICTORY

```
iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
```

# Level 5
```
Username: natas5
URL:      http://natas5.natas.labs.overthewire.org
```

![](/assets/15.png)

## Not logged in? Well, the answer is yummy. Sent the request to Burp's repeater..

![](/assets/16.png)

### What's this? Logged in boolean? Lets change and send.

![](/assets/17.png)

VICTORY
```
aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```

# Level 6
```
Username: natas6
URL:      http://natas6.natas.labs.overthewire.org
```

![](/assets/18.png)

### More secrets?!

![](/assets/19.png)

### Lets take a look 

![](/assets/20.png)

### Cool, copy, paste, and submit#

![](/assets/21.png)

VICTORY

```
 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
```

# Level 7

```
Username: natas7
URL:      http://natas7.natas.labs.overthewire.org
```

![](/assets/22.png)

### Well, that's useful. Let's look at the links. Ooooh, url parameters.

![](/assets/23.png)
![](/assets/24.png)

### Quick look at the source, just to make sure nothing odd is happening
![](/assets/25.png)

### Luckily, I remember how to do this.. Sooo file traversal is a thing. Just adding a lot of dot dot slahes to make sure I hit root.

![](/assets/26.png)

VICTORY

```
DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
```