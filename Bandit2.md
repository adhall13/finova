# Bandit Level 1 → Level 2

## Level Goal
The password for the next level is stored in a file called `-` located in the home directory

## Solve
```
bandit0@bandit:~$ exit
logout
Connection to bandit.labs.overthewire.org closed.
C:\Users\anuhy>ssh bandit1@bandit.labs.overthewire.org -p 2220
backend: gibson-0
bandit1@bandit.labs.overthewire.org's password:
Welcome to OverTheWire!

bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## What I learnt
The main lesson was how to handle unusual filenames that confuse the shell, and the proper procedure for progressing between levels.

Key points:

* **Handling Ambiguous Filenames (The Core Trick):** You learned that a filename consisting of only a dash (`-`) can be misinterpreted by commands (like `cat`) as a command-line option, causing the command to hang or read from standard input.
    * To force the shell to treat the dash as a filename, you must use a path prefix:
        * The relative path **`./-`** (meaning "the file named '-' in the current directory").
        * The special argument **`--`** (meaning "stop processing options; everything that follows is a filename"), used as **`cat -- -`**.
* **Level Progression Protocol:** You solidified the steps required to move from one user to the next:
    * After finding the password for the next user, you **need to exit** your current session (`exit`).
    * You must then **re-login using SSH** with the new username and the newly found password (e.g., `ssh bandit2@...`).
