# Bandit Level 8 → Level 9

## Level Goal 
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Commands you may need to solve this level: grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Solve
```
bandit8@bandit:~$ cat data.txt | sort | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## What I learnt
* I learned how to use the sort command to arrange text lines alphabetically, which is a required prerequisite for the uniq command to function correctly.
* I practiced using the uniq -u flag to filter a file and display only the lines that occur exactly once, removing all duplicate entries.
* I mastered the concept of "piping" (|) to chain multiple commands together, passing the output of cat into sort and then into uniq in a single operation.
