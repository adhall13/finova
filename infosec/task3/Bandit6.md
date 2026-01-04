# Bandit Level 5 → Level 6

## Level Goal 
The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:

human-readable
1033 bytes in size
not executable

## Solve
```
C:\Users\anuhy>ssh bandit5@bandit.labs.overthewire.org -p 2220
bandit5@bandit.labs.overthewire.org's password:
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls -a
.            maybehere03  maybehere08  maybehere13  maybehere18
..           maybehere04  maybehere09  maybehere14  maybehere19
maybehere00  maybehere05  maybehere10  maybehere15
maybehere01  maybehere06  maybehere11  maybehere16
maybehere02  maybehere07  maybehere12  maybehere17
bandit5@bandit:~/inhere$ find -type f -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## What I learnt
* I was able to learn how to implement the find to search through multiple subdirectories at once using a filter for a particular file size, which in my case was 1033 bytes, using the `-size` option.


