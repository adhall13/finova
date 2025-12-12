# Bandit Level 0 → Level 1

## Level Goal
The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

## Solve
```
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## What I learnt
The transition from Bandit Level 0 to Level 1 taught me how to navigate the basic Linux filesystem to find a password. Specifically:

* Use the **`ls`** command to **list files** in the current directory.
* Use the **`cat`** command to **read the contents** of a file (in this case, the `readme` file) to retrieve the password for the next level.
