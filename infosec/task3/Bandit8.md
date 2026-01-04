# Bandit Level 7 → Level 8

## Level Goal 
The password for the next level is stored in the file data.txt next to the word millionth

Commands you may need to solve this level: man, grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Solve
```
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ cat data.txt | grep millionth
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## What I learnt
* I learned how to use the `grep` command to search for a keyword within a file, thus to avoid searching through thousands of entries.
* I was able to apply the `pipe` operator to redirect the content of a file into a search tool.
* I understood how to handle large data files by targeting a unique identifier to isolate the password I needed.
