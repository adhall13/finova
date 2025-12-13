# Bandit Level 4 → Level 5

## Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.
Commands you may need to solve this level: ls , cd , cat , file , du , find

## Solve
```
C:\Users\anuhy>ssh bandit4@bandit.labs.overthewire.org -p 2220
backend: gibson-1
bandit4@bandit.labs.overthewire.org's password:
Welcome to OverTheWire!
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls -la
total 48
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file00
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file01
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file02
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file03
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file04
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file05
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file06
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file07
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file08
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file09
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: OpenPGP Public Key
./-file02: OpenPGP Public Key
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## What I learnt 
This level teaches me how to distinguish between different file types on a Linux system

1. **File Type Identification:** You learned to use the `file` command to determine the exact type of a file without viewing its contents i.e. `file <filename>`

2. **The Problem:** The `inhere` directory contains multiple files, but only one is human-readable; thus attempting to `cat` a binary or compressed file can "mess up" your terminal (display garbage characters), hence the "reset" tip.

3. **The Solution:** The `file` command helps you quickly spot the human-readable file among others that are typically:
    * **Data** (generic binary).
    * **Executable** (program files).
    * **ASCII text** (the one you need!).

**The Flow:**
    1.  `cd inhere`
    2.  `ls` (to see the file names, e.g., `file00`, `file01`, etc.)
    3.  `file *` (to check the type of **all** files at once)
    4.  `cat <human-readable-file>` (to retrieve the password)
