# Bandit Level 10 → Level 11

## Level Goal 
The password for the next level is stored in the file data.txt, which contains base64 encoded data

Commands you may need to solve this level: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Solve
```
C:\Users\anuhy>ssh bandit10@bandit.labs.overthewire.org -p 2220
bandit10@bandit.labs.overthewire.org's password:
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt | base64 --decode
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```

## What I learnt
* I learned how to use the `base64` command with the `-decode` or `-d` flag to decode a file, transforming scrambled ASCII strings into readable format.
