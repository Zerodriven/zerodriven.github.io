--
layout: post
date:   2021-04-07 21:21:00 +0100
categories: OverTheWire Bandit
---
#  On the last episode of Bandit..

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

## Lets take a look
```bash
bandit7@bandit:~$ ls
data.txt
```

## Lets open the file
```bash
...snip...
Lots of keys here
...snip...
```

## Okay, lets find unique ones...
```bash
bandit8@bandit:~$ sort data.txt | uniq
...snip...
07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
0N65ZPpNGkUJePzFxctCRZRXVrCbUGfm
zdd2ctVveROGeiS2WE3TeLZMeL5jL7iM
...snip...
#Lot of unique ones.. But.. Not just 1 unique one..
```

## Mkay, lets try counting unique ones...
```bash
bandit8@bandit:~$ sort data.txt | uniq --count
     10 07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
     10 0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
     10 0N65ZPpNGkUJePzFxctCRZRXVrCbUGfm
     10 0Xo6DLyK5izRqEtBA7sW2SRmlAixWYSg
     10 10XitczY5Dz7UMoseKIeFWSzzwQrylfw
     10 1ETSsKgjfQj1cJeFzXLJWzKzza3iWcJa
     10 1T6qw9I32d71cS3TTvwmVp1WsxPFDJ9I
     10 2bFz9F0yRwxGzVCZ4Er04bk00qfUrzWb
     10 2CxmtCkpNL5ZjuoNzAtShkPXf5T43W7s
     10 337o85y4OymIh99WPUtotkb114evfAkC
     10 33xpPQhjt4Q2mqtX4sCVRwH2Zyh82E8R
     10 4SMqyZZztep75cte6xxKpVL49pKUkV8N
     10 5AdqWjoJOEdx5tJmZVBMo0K2e4arD3ZW
     10 5cO8XuoQWrzsyeOWDht8zgUIVWSRDaeC
     10 6PF22p6O8TphCTZot9ApZx8VfGuo8rd5
     10 7KaMzgnYMUeMISP9vuT3Dvsc06qfqa9u
     10 7uhj3nhe4AS0esnnEZHBAZN67fJ8BFjM
     10 8jtZmvqp9PTi8tp1oybBM663NQH3fhII
     10 8NtHZnWzCA8HswoJSCU7Ojg8nP3eKpsA
     10 aR2QhaBoDMncvJqPWkvLXMzEx9meBIbX
     10 BccauS9LeE8NUz4HVLXUwE8M1LWisPlG
     10 bRnktwNdxFy2RPZIshXJikswwEzJGvJ9
     10 cIPbot7oYveUPNxDMhv1hiri50CqpkTG
     10 cR6riSWC0ST7ALZ2i1e47r3gc0QxShGo
     10 CUqLkjIo0Jz9fNgrjPxiPa7PGGC1wpTQ
     10 dGnfD2LoqTiO1MBf2vmqw1KKEWSHfMKJ
     10 dqd5wTVO1cVPJoEY7GGkCdGxG6ZYqW98
     10 dqnvnNxL4QR3ALq95ckhZwEpl77cRgF4
     10 DqPqVp8YCjZ1vFsclwRTg13EuSc2D52X
     10 dV0aGGhk6mB4ZJX1aTTluAUIvLWToTYr
     10 DxxLvJl6cGHXLT7OW4xqS7Qrfny1K01l
     10 e5HFl4ur1rAxPPv2mHzg1uYKMuos4fwp
     10 Ef509iQpb5gQJsjz5dMXLxpeAfkbLOrw
     10 eTHlmI3pFZ4FQASs32Dm0ETVZWHlP0I1
     10 f0tri5KLH5eiTU0zQOqWvXTsrl1ekqnU
     10 f6ZuiZizTliaMOkVYXZMudtaReSYMnkP
     10 flyKxCbHB8uLTaIB5LXqQNuJj3yj00eh
     10 g1VkH2pk3cmr6aY4np1Dcpm0HF7G9IDT
     10 g9xRXSlVNiV4EhUAl1p6uPUWcyEewDK6
     10 gqyF9CW3NNIiGW27AtWVNPqp3i1fxTMY
     10 h2IsJoN6fe0ne0qrTQxeiu0P44hMWWbk
     10 hA6Ofhj75FPgqnCKEJ9g6pLSKapxxmGC
     10 Hq6uxRAkKPNLnH6eRSFDzXtvVt0CSsee
     10 I3fc578VLa7mOQ1t9zArPPOPY7aDVBcJ
     10 iIaOHQG7ZLdimomwMQaGIF7vib1RmXBh
     10 IkAAyqo1rCrxdY8qH0FfxXkRTTO2GNSf
     10 iKiMcQpNMn2ImOASX39XBUR8XfApdmsj
     10 InU7h0xhZh4SMMOMvlnsq03pz0k9J5FX
     10 iwE0KTeKQ8PWihqvjUnpu52YZeIO8Pqb
     10 J6Lzp6ZqTJsOuJRTXcvhwKfM0KK3Xtbl
     10 K9D1CLsVCdkodgvJJIt1oHIaiOY1h8hg
     10 KASHOxc1NxaM8caXUw5MHCkddANXOkCu
     10 khecG2RClunkhrgmq4UNB26N5F1yiUwL
     10 kJTBMD8k9OHyXwZ2aJMQkV23u0gyuoIO
     10 KLu6irnqFwhOKnVoTwuoT9e5t6oxYQwv
     10 KrDVVORXLPfRhfnRmmuP3OnVHWKDMSM8
     10 kUbOkhsIw6GSp0WI2YUo1Q3hDxFU0iQn
     10 l1I3Red7uSH9n30OylHP2hQDbOU0qGaq
     10 l2lECnJkQk8EBl6IO3gHUlnjoCTF1has
     10 LfrBHfAh0pP9bgGAZP4QrVkut3pysAYC
     10 Lg4vWWvEY7s0bG6BRiA35AHzo2gM6lHg
     10 mpgNGRH628hTQxajScbagkxaPKklUhjn
     10 mzOW32HQZi14kwrdeiquO1LCbyaOtbiT
     10 nJRb4MipHMdTmFylFc1NlqmywgxDSdoI
     10 NLWvtQvL7EaqBNx2x4eznRlQONULlCYZ
     10 NOdH1kFWibx4XnNaJoLFmghBn7oIs5hb
     10 ojGabNG5NJ9ppKUBXGr8lwMRRS5GuiA5
     10 OZ1wgx8bDI0vFOFxDQH32eMMcIPiIuPE
     10 PfbMe4Xb3mw5mJmabIbKAXKCU7zynDHl
     10 PQKOeIQwTw490Y8yobuxZAOL4cNmVo1D
     10 PSdVQSeUUBPRZD58WWP0OXLKxSgU3RxX
     10 ptb5ZW8TcgD3U6gOGCcN31xCDGIoQSEa
     10 qaWWAOOquC3yHnfJI4zvPWzCBdfHQ8wa
     10 RMiSPoAvF7WhgIcOdSQR2r6Zx0DNS5UW
     10 s1603Q2r4RPKqyoA8cspIRk0VdgEmFC3
     10 SA05uWMVCao2rzS8YRqUXh19SvnDpuOl
     10 SHMAMUEzQe4mV7SJpETTZFsyNRJsZE2k
     10 si952kS1y6pt4AFenmm0oIp8n7W5d3bd
     10 sYSokIATVvFUKU4sAHTtMarfjlZWWj5i
     10 SzwgS2ADSjP6ypOzp2bIvdqNyusRtrHj
     10 TKUtQbeYnEzzYIne7BinoBx2bHFLBXzG
     10 TThRArdF2ZEXMO47TIYkyPPLtvzzLcDf
     10 tVW9iY1Ml0uHPK4usZnN8oZXbjRt2ATY
     10 U0NYdD3wHZKpfEg9qGQOLJimAJy6qxhS
     10 UASW6CQwD6MRzftu6FAfyXBK0cVvnBLP
     10 UJiCNvDNfgb3fcCj8PjjnAXHqUM63Uyj
     10 UjsVbcqKeJqdCZQCDMkzv6A9X7hLbNE4
      1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
     10 UVnZvhiVQECraz5jl8U14sMVZQhjuXia
     10 V2d9umHiuPLYLIDsuHj0frOEmreCZMaA
     10 v9zaxkVAOdIOlITZY2uoCtB1fX2gmly9
     10 VkBAEWyIibVkeURZV5mowiGg6i3m7Be0
     10 w4zUWFGTUrAAh8lNkS8gH3WK2zowBEkA
     10 WBqr9xvf6mYTT5kLcTGCG6jb3ex94xWr
     10 wjNwumEX58RUQTrufHMciWz5Yx10GtTC
     10 X1JHOUkrb4KgugMXIzMWWIWvRkeZleTI
     10 XyeJdbrUJyGtdGx8cXLQST0pwu5cvpcA
     10 yo0HbSe2GM0jJNhRQLxwoPp7ayYEmRKY
     10 ySvsTwlMgnUF0n86Fgmn2TNjkSOlrV72
     10 Z9OC6DQpppreChPhwRJJV9YYTtrxNVcO
     10 zdd2ctVveROGeiS2WE3TeLZMeL5jL7iM
	 #There's a 1! There's probably a better way to do this though.
```

## Lets try a cleaner way, a bit of trial and error later
```bash
bandit8@bandit:~$ sort data.txt | sort | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

## The password for level 9:

UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR


## Connect to level 9.
```bash
bandit8@bandit:~$ ssh bandit9@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
