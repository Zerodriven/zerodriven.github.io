#  On the last episode of Bandit..
### Connecting to another username on the same server.

```bash
bandit1@bandit:~$ ssh bandit3@localhost
#Accept the fingerprint ('yes') and enter the password.
```

# Level goal
```bash
## Level Goal

The password for the next level is stored in a hidden file in the **inhere** directory.

## Commands you may need to solve this level

ls, cd, cat, file, du, find
```

## Lets look at all the files

```bash
bandit3@bandit:~$ ls
inhere
```

## Lets go into the directory

```bash
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$
# cd: change current working directory - Universal. 
```

## Lets look in here

```bash
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$
#Oh yeah, they're hidden! Lets show all the things.
bandit3@bandit:~/inhere$ ls -a
#  ls -a: list all files including hidden file starting with '.'
.  ..  .hidden
```

## Lets look in the hidden file
```bash
bandit3@bandit:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

## The password for level 4:

pIwrPrtPN36QITSp3EQaw936yaFoFgAB

## Connect to level 4.
```bash
bandit3@bandit:~$ ssh bandit4@localhost
#Accept the fingerprint ('yes') and enter the password.
```

On the next episode of Bandit...