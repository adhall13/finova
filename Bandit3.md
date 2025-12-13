# Bandit Level 2 → Level 3

## Level Goal
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

## Solve
```
C:\Users\anuhy>ssh bandit2@bandit.labs.overthewire.org -p 2220
backend: gibson-1
bandit2@bandit.labs.overthewire.org's password:
bandit2@bandit:~$ cat "./--spaces in this filename--"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## What I learnt
To solve, I learned that the Linux shell treats spaces as separators between different commands or arguments. 
To treat a filename with spaces as a single item, you have three main methods:

* **Quotes:** Wrap the name in quotes so the shell reads it as one string. e.g.
  `cat "spaces in this filename"`
* **Backslashes (`\`):** "Escape" each space to tell the shell it is part of the name. e.g.
  `cat spaces\ in\ this\ filename`
* **Tab Completion:** Type `cat` and the first few letters, then press **Tab**. The shell will automatically add the backslashes for you.

The `./` represents the current directory. Using it (`cat ./filename`) explicitly tells the system to look for the file in your active folder. 
This is especially helpful if a filename starts with a dash (`-`), which the system might otherwise mistake for a command option.
