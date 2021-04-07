#  On the last episode of Bandit..

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
The password for the next level is stored in the file **data.txt** next to the word **millionth**

## Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd
```

## Lets take a look
```bash
bandit7@bandit:~$ ls
data.txt
```

## I'm not going to open the data.txt file here.. There's a lot of info in it... So lets look at the word millionth.

```bash
bandit7@bandit:~$ grep millionth data.txt
millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV

```

## The password for level 8:

cvX2JJa4CFALtqS87jk27qwqGhBM9plV


## Connect to level 8.
```bash
bandit7@bandit:~$ ssh bandit8@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...
