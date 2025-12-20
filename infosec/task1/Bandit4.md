# Bandit Level 3 → Level 4


## Level Goal
The password for the next level is stored in a hidden file in the inhere directory

## Solve
```
C:\Users\anuhy>ssh bandit3@bandit.labs.overthewire.org -p 2220
backend: gibson-1
bandit3@bandit.labs.overthewire.org's password:
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
bandit3@bandit:~/inhere$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

## What I learnt
* **Hidden Files:** Files and directories that start with a dot (`.`) are hidden from standard directory listings.
* **The `ls -a` Command:** The **`-a`** (for "all") option for the `ls` command reveals these hidden files, allowing you to find the password stored inside the `inhere` directory.
