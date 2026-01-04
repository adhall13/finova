# Bandit Level 9 → Level 10

## Level Goal 
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several `=` characters.

## Solve
```
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ strings data.txt | grep =
========== the
9=H`
[!#=Z
========== password
xWf=
f\Z'========== is
e=i{\#
/1=s
nS=F
M=Sl
=LGT
y =1
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
'+Y=+
```

## What I learnt
* I learned how to use the `strings` command to extract sequences of printable characters from a binary file, effectively filtering out the data that usually crashes a terminal.
* I used `grep` to search for patterns within those extracted strings, specifically looking for the "=" prefix to pinpoint the exact location of the password.
