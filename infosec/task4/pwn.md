# File Globbing

## Matching with *
The challenge requires you to change directory from your home into the absolute path `/challenge` while making sure the single argument you pass to `cd` is no more than four characters long, and then run `/challenge/run` to get the flag.

## How to solve the challenge
Type a compact glob that the shell will expand to `/challenge` — for example, `/ch*`. When the shell performs pathname expansion, it will match entries in the root directory whose names start with `ch`, and `/ch*` will expand to `/challenge`, so `cd /ch*` changes you into `/challenge`. Once there, run the provided program `/challenge/run` to obtain the flag.

code:
```
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ echo /c*
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
/challenge
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /c*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{IW-znbWF-HEBMo48h9FzdP3-09q.QXxIDO0wiMwEzNzEzW}
```

Explanation: /c* is 3 characters; the shell expands /c* to /challenge (assuming /challenge is the only root entry starting with c). echo /c* shows what will be used before you cd. If the echo prints /c* unchanged, your shell's globbing might be configured not to expand unmatched patterns — but on the challenge system /c* should expand to /challenge.

## What I learnt
I learnt that the exercise depends on filename globbing: `*`. It is a wildcard that matches any sequence of characters except `/` and a leading `.`. The shell expands globs before invoking a command, and a short glob can expand to a longer path — letting you meet the “four-character argument” constraint even though the real pathname is longer. Also note that globs can match zero, one, or many files; here, you rely on a pattern that uniquely matches the desired directory in the filesystem.

## References
None used for this challenge


## Matching with ?
The task is to change directory from your home into the absolute path `/challenge` while using the single-character glob `?` in place of the letters `c` and `l` in the argument you pass to `cd`, then run `/challenge/run` to get the flag.

## The Solve
Type a `cd` command that uses `?` for each of the specified characters so the shell’s pathname expansion produces `/challenge`. For example: `cd /?ha??enge` — here the first `?` stands for `c` and the two `?`s stand in for the two `l` characters; the shell expands `/​?ha??enge` to `/challenge` and `cd` moves you there. After changing the directory, run `/challenge/run` to retrieve the flag.

code:
```
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ echo /?ha??enge
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
/challenge
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
This challenge resets your working directory to /home/hacker unless you change 
directory properly...
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{YFpj4gfqxRl2BR8uPtWXiyLQ4vf.QXyIDO0wiMwEzNzEzW}
```

## What I learnt
This exercise taught me single-character globbing: `?` matches exactly one character (not `/` and not a leading `.`). Multiple `?`s can be used to match multiple single characters in specific positions, letting a short pattern expand into a longer filename or path. The shell performs glob expansion before running the command, so you can type a pattern that looks different from the final pathname but still resolves to the target directory.

## References
None used for this challenge


## Matching with []
In this challenge, you are asked to change your working directory to `/challenge/files` and then run `/challenge/run`. However, you need to use a glob pattern with square brackets `[]` to match a specific set of files — specifically, `file_b`, `file_a`, `file_s`, and `file_h` — all with a single argument. This requires to craft a pattern using square brackets that includes the characters needed to match the filenames to use.

## The Solve
To solve this, you'll need to identify the common pattern in the filenames and use square bracket globbing to match them. The pattern you need is `file_[bahs]`, where the square brackets allow you to match any one of the characters `b`, `a`, `h`, or `s` in place of the last character of the filename. This will match the filenames `file_b`, `file_a`, `file_s`, and `file_h`. Once you're in the right directory, running the command `/challenge/run` will give you the flag.

code:
```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ echo Look: file_[bash]
Look: file_a file_b file_h file_s
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[bash]
You got it! Here is your flag!
pwn.college{s0TCOgbLRGZn7Lwflxpz1c33DZr.QXzIDO0wiMwEzNzEzW}
```

## What I learnt
The challenge revolves around using the square brackets `[]` for pattern matching in filenames. Unlike `?`, which matches exactly one character, `[]` allows you to specify a range or set of characters that can match any one of them. For example, `[pwn]` will match any of the characters `p`, `w`, or `n`. This makes `[]` a more flexible tool compared to `?`, as you can precisely control which characters can appear in a given position of the filename. 

## References
None used for this challenge


## Matching Paths with []
For this challenge, run `/challenge/run` from your home directory with a single argument that, after shell globbing, becomes the absolute paths to `file_b`, `file_a`, `file_s`, and `file_h` in `/challenge/files`. Thus, you must provide one bracket-globbed argument that the shell expands into the four full paths under `/challenge/files`.

## The Solve
To solve this, we use a glob pattern that matches the four specific files. You will use square brackets `[]` to specify a set of characters that can match the final character in the filenames. The pattern you choose should be able to match all the necessary files in `/challenge/files` by expanding to their absolute paths when used as an argument in the run command.

code:
```
hacker@globbing~matching-paths-with-:~$ echo /challenge/files/file_[bash]
/challenge/files/file_a /challenge/files/file_b /challenge/files/file_h /challenge/files/file_s
hacker@globbing~matching-paths-with-:~$ /challenge/run /challe
nge/files/file_[bash]
You got it! Here is your flag!
pwn.college{ErSsiVsGhCbi3Q3jrc5wY4M2PaV.QX0IDO0wiMwEzNzEzW}
```

## What I learnt 
Globbing operates per pathname component and is performed by the shell before a program is executed. Using `[]` lets you specify a range of characters that match exactly one character in that position, so a single bracket pattern can generate multiple filenames. Because you provided an absolute path with the bracket expression in the final component, the shell expands it into absolute filenames under `/challenge/files`, satisfying the requirement to pass the expanded absolute paths to `/challenge/run`.

## References
None used for this challenge


## Multiple Globs
The challenge requires you to navigate to `/challenge/files` and run `/challenge/run`, but you will need to provide a single, short glob pattern that includes two `*` wildcards. This pattern must expand to match all filenames in the directory that contain the letter `p`. Essentially, the shell will expand your small pattern into every file with `p` in its name, and those expanded file paths will be passed as arguments to `/challenge/run`.

## The Solve
Pick a compact pattern with two asterisks and the letter `p` between them so the shell will match any filename containing `p` anywhere in its name. The natural three-character choice is `*p*`; when the shell performs pathname expansion, it will replace that single argument with every filename in the current directory that includes `p`, and then `/challenge/run` will be invoked with those matched filenames.

code:
```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ echo *p*
happy optimistic pwning splendid uplifting
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{sVm5KUZzdDzyYaI2xjNk_P0xYwh.0lM3kjNxwiMwEzNzEzW}
```

## What I learnt
I learnt that it relies on multiple glob expansion inside a single word: a single argument may contain more than one `*` and the shell expands it before executing the command. The `*` wildcard matches any sequence of characters (except `/`), so `*p*` finds names with `p` anywhere. Globbing is performed by the shell on path components, and the result — zero, one, or many filenames — is what the receiving program actually gets.

## References
None used for this challenge


## Mixing Globs
In this challenge, we change into `/challenge/files` and run `/challenge/run` with a single, short glob pattern. This glob must match the filenames `challenging`, `educational`, and `pwning` when expanded by the shell. 

## The Solve
To solve this, you'll need to use globbing to match all three filenames within the 6-character limit. A possible solution would be using the pattern `*ing`. This works because the suffix `ing` is common to all three filenames, and the leading `*` matches any characters before it. The shell will expand `*ing` to match `challenging`, `educational`, and `pwning` when you run the `/challenge/run` command with that argument.

code:
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]
Your expansion did not expand to the requested files (challenging, educational, 
pwning). Instead, it expanded to:
[cep]
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{EIqyHyjztCDLuYqzZqC1m0UvDC5.QX1IDO0wiMwEzNzEzW}
```

## What I learnt
I learnt that this challenge brings together multiple globbing concepts: using `*` to match any sequence of characters and narrowing the match with a specific suffix. The pattern `*ing` leverages the power of `*` to match any prefix before the `ing` suffix, which is common to all three target filenames. The shell expands this glob pattern before executing the command, and the result is passed as an argument to `/challenge/run`. 

## References
None used for this challenge


## Exclusionary Globbing
In this challenge, you're tasked with running `/challenge/run` from `/challenge/files`, but you must provide a glob pattern that matches all files in the directory except those that start with the letters `p`, `w`, or `n`. 

## The Solve
To solve this, you'll use the `[]` globbing feature to exclude files that start with `p`, `w`, or `n`. By using the `!` or `^` character inside the brackets, you can invert the match. For example, the pattern `file_[!pwn]*` or `file_[^pwn]*` will match all files that do not begin with `p`, `w`, or `n`. This way, when the shell expands the glob, it will pass only the filenames that don't start with those letters as arguments to `/challenge/run`.
code:
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{sGdct-pUkZ1tTz94FAR5KXETGgd.QX2IDO0wiMwEzNzEzW}
```

## What I learnt
The key concept here is the use of negation in globbing with the `!` or `^` character inside square brackets `[]`. When placed as the first character in the brackets, these symbols reverse the match, meaning the glob will match any character except those listed. This allows you to filter out specific files based on their starting letters. Additionally, it's important to remember that `!` has different meanings in bash depending on context, so using `^` is a more universally compatible approach for newer versions of bash. The ability to filter out files using globbing is a powerful tool for refining file matching.

## References
None used for this challenge


## Tab Completion
You must read a flag that was placed under `/challenge` but you are prevented from typing the real filename directly because it contains trickery (hidden or unusual characters). The directory listing shows a name that looks like `pwncollege`, and `cat` of that literal name fails; instead you are required to use your shell’s tab-completion to expand an abbreviated prefix into the actual filename so you can `cat` it and see the flag.

## The Solve
Change nothing about the file system — instead type a short unambiguous prefix of the name (for example `pwn`) and press the Tab key. The shell’s completion mechanism will query the filesystem and insert the exact filename, including any characters you cannot easily type or see. Once the name has been expanded by Tab you can run `cat` (or otherwise read the file) and the command will succeed because it now references the real filename the kernel knows about.

code:
```
hacker@globbing~tab-completion:~$ ls /challenge
DESCRIPTION.md  pwncollege​
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{wTfbp6pxnMppN6NKLITDkpioxmW.0FN0EzNxwiMwEzNzEzW}
```

## What I learnt
This exercise demonstrates shell tab-completion (readline/programmable completion) as a safer and more reliable way to specify filenames than guessing or using wildcards. Completion uses the filesystem’s actual names, so it will reveal and insert characters that may be invisible or awkward to type (control characters, punctuation, unusual Unicode, etc.), avoiding mistakes caused by glob expansion or manual typing.

## References
None used for this challenge


## Multiple Options for Tab Completion
You need to find and read the flag that lives under `/challenge/files`, but the directory contains many filenames that share the same initial letters. The challenge requires you to use your shell’s tab-completion starting from a prefix like `/challenge/files/p` to navigate the many similarly-named entries and ultimately complete the correct filename so you can read the flag.

## The Solve
Type the path up to a reasonable prefix (for example `/challenge/files/p`) and hit Tab. Because multiple filenames match that prefix, your shell will either expand up to the common characters among all matches and then stop (bash’s default) or begin cycling through choices depending on configuration. If the first Tab stops at the longest unambiguous prefix, hit Tab again to list the options; inspect the list and continue typing more characters of the desired name or use additional Tab presses to complete the exact filename. Once the filename is fully expanded by completion, run the command to read the file and retrieve the flag.

code:
```
hacker@globbing~multiple-options-for-tab-completion:~$ cat /challenge/files/pwncollege-flag
pwn.college{oN_H_KC1kw_ji1IrYElsxakJ6Us.0lN0EzNxwiMwEzNzEzW}
```

## What I learnt
This exercise highlights how programmable completion behaves when multiple candidates exist: some shells (or bash defaults) expand only up to the shared prefix and require a second Tab to show choices, while others cycle through alternatives. Tab-completion reveals the true exact filename from the filesystem (including characters you might not want to type manually), helps avoid mistakes from wildcards, and is an interactive tool for disambiguating many similarly-named files. Understanding how your shell responds to single vs. repeated Tab presses is essential for efficiently locating and completing the correct target.

## References
None used for this challenge


## Multiple Options on Command
The task is to invoke a hidden program whose name begins with `pwncollege` by using your shell’s command-name tab-completion. The program will print the flag when executed, but you’re not expected to type the whole command name by hand; the shell will auto-complete.

## The Solve
Start typing the beginning of the program name (`pwncollege`) at the shell prompt and press the Tab key. The shell’s completion system will fill in the rest of the command name; once the name is completed, hit Enter to run it and read the flag. 

Type `pwncollege` and press tab to autofill the command, and press enter to get the flag
code:
```
hacker@globbing~tab-completion-on-commands:~$ pwncollege-8310 
Correct! Here is your flag:
pwn.college{omvdNFY-pb7ZUfrcRspEW-EvgQE.0VN0EzNxwiMwEzNzEzW}
```

## What I learnt
Tab completion works for more than filenames: the shell also completes command names using entries found in the PATH. Completion reduces typing and prevents errors by inserting the exact executable name the system will call. 

## References
None used for this challenge


# Practicing Piping

## Redirecting Output 
The challenge is simple and specific: use shell output redirection to write the exact string `PWN` (uppercase) into a file named `COLLEGE` (uppercase). 

## The Solve
The straightforward solution is to run a shell command that emits `PWN` and redirect that output into the file `COLLEGE`
code:
```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{MzoOJmTpFbk_DEUTGmqbR4uUwOJ.QX0YTN0wiMwEzNzEzW}
```

## What I learnt 
This exercise reinforces core shell concepts: how `>` redirects and truncates or creates files, the difference between `>` and `>>` (overwrite vs append), how commands like `echo` and `printf` produce stdout, and that filenames and payloads are case-sensitive on typical Unix-like systems (so `COLLEGE` ≠ `college`). It also highlights small practical details — `echo` may add a newline, shell expansions or quotes can change the output, and file permissions/environment affect whether redirection succeeds — all useful basics for safe, predictable shell scripting and operations. 

## References
None used for this challenge


## Redirecting More Output 
The challenge asks to redirect the output of the /challenge/run command to a file named `myflag`, capturing the flag, while ensuring that instructions and feedback (printed to stderr) still appear on the terminal.

## The Solve
 You can redirect just the `stdout` (where the flag is printed) to the file `myflag` using: `/challenge/run > myflag`. This keeps the `stderr` visible in the terminal while saving the flag in the file.

code:
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{oyFrN7X8C5GTnBdLLwGLZvTrRkr.QX1YTN0wiMwEzNzEzW}
```

## What I learnt
This exercise drills the crucial distinction between `stdout` and `stderr` and when to capture one stream but not the other. It reinforces that `>` only affects `stdout`, that `2>` targets `stderr`, and that `2>&1` merges streams. Practically, it’s a useful pattern: capture machine-readable output to files while keeping human-readable errors and prompts visible — a technique common in scripting, logging, and debugging.

## References
None used for this challenge


## Appending Output
The challenge asks to run `/challenge/run` so that its output is appended to the file `/home/hacker/the-flag` (not overwritten). The program writes the first half of the flag into the file and the second half to `stdout`; if you use truncation (`>`), the second half will overwrite the first, and you’ll lose half the flag — so you must use append mode.

## The Solve
code:
```
hacker@piping~appending-output:~$ /challenge/run >> /home/hacker/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat /home/hacker/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{cDwoQ1glwWKoYG_CnBi9mP2S3TR.QX3ATO0wiMwEzNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
hacker@piping~appending-output:~$ 
```

## What I learnt
This reinforces the difference between `>` (truncate/create) and `>>` (append) and why append is essential when aggregating outputs across multiple runs. It’s a practical reminder to choose redirection mode carefully to avoid unintentionally destroying previously collected data, and to check file permissions and confirm results after redirection.

## References
None used for this challenge


## Redirecting Errors
The level requires you to capture the flag into a file named `myflag` and capture everything it prints to standard error into a separate file named `instructions`. Because both streams must be redirected, nothing should be left printing to the terminal — the flag should end up in `myflag` and the instructions in `instructions`.

## The Solve
Run the program and explicitly redirect FD 1 (stdout) and FD 2 (stderr) to the two files. Verify with `cat myflag` to read the flag and `cat instructions` to read the program’s messages. Ensure you have write permission in the current directory so both files can be created/overwritten.

code:
```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2>
 instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{EmE9zG_Ji7L1D9l0E8Z93Alo_Ez.QX3YTN0wiMwEzNzEzW}
```

## What I learnt
This exercise reinforces how Linux uses file descriptors (0,1,2) for stdin/stdout/stderr, how `>` without a number implies `1>`, and how to redirect multiple FDs at once. It shows a practical pattern: separate machine-readable output (stdout) from human-readable errors/prompts (stderr) into different files, which is useful for logging, automated parsing, and debugging.

## References
None used for this challenge


## Redirecting Input
The level requires supplying the program’s standard input from a file named `PWN`, and that `PWN` file must contain the exact text `COLLEGE`. 

## The Solve
Create the file `PWN` and put the exact word `COLLEGE` into it (overwriting any previous contents). Then invoke the challenge so that its standard input comes from the `PWN` file. 
code:
```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{IHINM8VBJE_Ih8xYoGU7bzD_FD8.QXwcTN0wiMwEzNzEzW}
```

## What I learnt 
This challenge highlighted the power of input redirection, showing how programs can read from files instead of waiting for manual input. It also reinforced the importance of precision when specifying filenames and content, particularly with case sensitivity and avoiding extra characters. Additionally, I learned how input and output redirection can be combined effectively to automate tasks and streamline processes in the command line.

## References
None used for this challenge


## Grepping Stored Results
The challenge asks you to capture the output of a program (`/challenge/run`) into a file and then locate the single line among ~100,000 lines that contains the flag.

## The Solve
code:
```
hacker@piping~grepping-stored-results:~$  /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$  grep pwn /tmp/data.txt
pwned
pwning
pwn
pwn.college{U5svksqVrXngdkTCA6bl6HD-YyI.QX4EDO0wiMwEzNzEzW}
pwns
```

## What I learnt
This exercise reinforces basic but essential shell skills: redirection (`>`), understanding stdout vs stderr (stdout is the normal output of a program, while stderr is used for error messages), and powerful text processing with `grep` and regular expressions. 

## References
None used for this challenge


## Grepping Live Output
The challenge asks to capture the output of `/challenge/run` and find the single line that contains the flag, but instead of saving to a file first, you must use a pipeline so the program’s stdout flows directly into a searching tool.

## The Solve

code:
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{0sIIvIV7S9yz45qwi81q6IVGrjs.QX5EDO0wiMwEzNzEzW}
```

## What I learnt 
Pipes let you process large outputs in‑memory without creating temporary files, making workflows simpler and faster. `grep` with a regex extracts the flag pattern directly.

## References
None used for this challenge


## Grepping Errors
The challenge asks to extract specific information from standard error (stderr) output by redirecting it to standard output (stdout) and then piping the combined output to a program like `grep` for further searching. 

## The Solve
code:
```
hacker@piping~grepping-errors:~$ /challenge/run 2>& 1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{IKYXFphvtiwmoTAmTfvMKMSula2.QX1ATO0wiMwEzNzEzW}
```

## What I learnt
This challenge taught me how to combine redirecting output and error streams using the `2>&1` operator.  
`2>&1`: redirects standard error to standard output; 

## References
None used for this challenge


## Filtering with Grep -v
The challenge gives a command `/challenge/run` that prints the real flag mixed together with over a thousand decoy flags — every decoy contains the literal string `DECOY` somewhere in the line; for this challenge, extract the single real flag from all the decoy lines. 

## The Solve
code:
```
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v 'DECOY'
pwn.college{os6mawOpkz-61Ckib1-FTbLopr5.0FOxEzNxwiMwEzNzEzW}
```

## What I learnt
This exercise reinforces how powerful simple Unix text tools are when combined with pipes: `grep -v` is an easy way to invert selections and remove unwanted decoys (noise) from data (stream) instead of trying to pick the one correct line out of thousands. Beware that an inverted filter will drop any line containing the pattern (so if the real flag ever contained the same token, we need a different approach).

## References
None used for this challenge


## Duplicating Piped Data with Tee
The challenge requires running the two-process pipeline while also inspecting the data that flows from `pwn` so you can discover what `pwn` is asking for and then provide the correct input to make the overall pipeline succeed. 

## The Solve
code:
```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee /tmp/pwn_output.txt | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat /tmp/pwn_output.txt
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "kGTwN1KI"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret kGTwN1KI | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{kGTwN1KIRQ1A8KF8i_Vw5oPgvDG.QXxITO0wiMwEzNzEzW}
hacker@piping~duplicating-piped-data-with-tee:~$
```

## What I learnt
The task taught me that `tee` is a straightforward tool to make a pipeline observable without interrupting data flow. Moreover, `tee` only mirrors stdout unless you redirect stderr, `-a` appends instead of overwriting, and captures intermediate output.

## References
None used for this challenge


## Process Substitution for Input
The challenge asks us to identify the real flag hidden among several decoy flags by comparing the outputs of two programs: `/challenge/print_decoys`, which prints a list of decoy flags, and `/challenge/print_decoys_and_flag`, which prints the same decoys along with the real flag. 

## The Solve

code:
```
hacker@piping~process-substitution-for-input:~$ diff <( /challenge/print_decoys ) <( /challenge/print_decoys_and_flag )
43a44
> pwn.college{06n1VhzR_Pdil2DJ2yVe9T3gUYH.0lNwMDOxwiMwEzNzEzW}
```

## What I learnt 
Through this challenge, I learnt the shell adheres to this by allowing us to treat not only traditional files but also the input and output of programs as file-like objects. This concept becomes especially powerful with Process Substitution, which enables us to hook the output of a command directly to the input of another, bypassing the need for temporary files. By using `<(command)`, we can treat the output of a command like a file, and with `(command)`, we can feed input to a command as if it were coming from a file. This capability makes it possible to seamlessly connect commands and utilities, allowing for more efficient and elegant workflows in the shell.


## References
None used for this challenge


## Writing to Multiple Programs
This challenge asks us to duplicate the output of the `/challenge/hack` command and pipe it as input to two other commands, `/challenge/the` and `/challenge/planet` without needing temporary files. 

## The Solve

code:
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >( /challenge/the ) >( /challenge/planet )
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
11967155301869310305
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{QA9VbphefINLlDjYBMk5Utwj7mQ.QXwgDN1wiMwEzNzEzW}
```
process:
- /challenge/hack outputs data.
- tee reads that output and duplicates it.
- One copy goes to /challenge/the via the first >(...).
- The other copy goes to /challenge/planet via the second >(...).
- tee also sends a copy to its standard output, but since you didn't redirect that, it just prints to your terminal (you can ignore or redirect it if needed).

## What I learnt 
Through this challenge, I gained a deeper understanding of how process substitution can be used not just for reading data, but also for writing data to commands. I learned how to combine `tee` with output process substitution to duplicate data to multiple commands at once. 

## References
None used for this challenge


## Split-piping stderr and stdout
In this challenge, need to redirect the output from the `/challenge/hack` command to two separate programs, `/challenge/the` and `/challenge/planet`. Specifically, the challenge asks you to send `stderr` (standard error) to `/challenge/the` and `stdout` (standard output) to `/challenge/planet`. The key difficulty here is keeping these two streams separate while still using shell piping.

## The Solve
code:
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{E91OaHum_jIXt6njBk8prtmzO3K.QXxQDM2wiMwEzNzEzW}
```

## What I learnt 
This challenge deepened my understanding of how to manipulate file descriptors in Unix-like systems. I learned how to use `2>`, `>(...)`, and `|` together to separate `stderr` and `stdout` and send them to different destinations. The power of process substitution became clear, as it allowed me to route `stderr` to a command without mixing it with `stdout`. I also reinforced the importance of understanding how file descriptors work in shell scripting, which is crucial for advanced tasks like managing multiple output streams.

## References
None used for this challenge


## Named Pipes
The challenge asks to create a persistent named pipe (FIFO) at `/tmp/flag_fifo` and then redirect the stdout of `/challenge/run` into that FIFO so that `/challenge/run` will write the flag into it. 

## The Solve
code:
```
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!
----------------------------------------------------------------------------
hacker@piping~named-pipes:~$  cat /tmp/flag_fifo
You've correctly redirected /challenge/run's stdout to a FIFO at
/tmp/flag_fifo! Here is your flag:
pwn.college{MbHdj-mVp10Kc1SiOyAui11b-A_.01MzMDOxwiMwEzNzEzW}
```

## What I learnt 
This exercise reinforced how FIFOs (mkfifo) let processes communicate through a filesystem-visible pipe: they don’t store data on disk, data is ephemeral (consumed once), and reads/writes automatically synchronize because operations block until the other side is ready. FIFOs are handy for orchestrating complex workflows or connecting multiple readers/writers without temporary files, but you must manage blocking behavior (use separate terminals or background processes) and clean up the FIFO when finished.

## References
None used for this challenge


# Shell Variables

## Printing Variables
The challenge hides the flag in a shell variable named FLAG instead of letting the provided program return it. We have to print the contents of that environment variable from the current shell to read the flag directly.

## The Solve
Use a command that prints text to standard output and reference the variable with a leading dollar sign; for example, run `echo $FLAG` in your shell. The shell will substitute the value stored in `FLAG` before `echo` runs, and the variable’s contents (the flag) will be printed to the terminal. If you prefer, other printing utilities like `printf` will work as well, but `echo $FLAG` is the simplest.

code:
```
hacker@variables~printing-variables:~$ echo "$FLAG"
pwn.college{88pvETaZUhs75lwPTchr7TFAxBs.QX3UTN0wiMwEzNzEzW}
```

## What I learnt
This exercise teaches me about shell variables and parameter expansion: a `$` before a name tells the shell to replace that token with the variable’s value before running the command. It also highlights that the environment available to your interactive shell can hold secrets (like `FLAG`) separate from what a particular program returns, and that simple built-in commands can be used to inspect those variables.

## References
None used for this challenge


## Setting Variables
For this challenge, create a shell variable named `PWN` and assign it the exact value `COLLEGE`. 

## The Solve
Assign the value to the variable using the shell’s assignment syntax: the variable name, an equals sign with no surrounding spaces, and the value. After that, you can read the variable using the `$` prefix to confirm it holds the expected value. Remember that the `$` is only used when accessing a variable, not when creating it.

code:
```
hacker@variables~setting-variables:~$ PWN=COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{w3i3kK9Oqc3OgEttaH_PZCECzUh.QX5UTN0wiMwEzNzEzW}
```

## What I learnt
This exercise taught me that the challenge reinforces shell variable assignment and expansion: `NAME=VALUE` creates or changes a shell variable, and `$NAME` expands to its value. Important gotchas are that there must be no spaces around the `=` and that both variable names and values are case-sensitive. Also note the distinction between assigning a shell variable and exporting it to the environment — a plain assignment lives in the current shell unless you explicitly export it. Also revised the concept of shell being case-sensitive. 

## References
None used for this challenge


## Multi-word Variables
The challenge asks you to set a variable in the shell, but with a value that contains spaces. Specifically, asked to assign the value "COLLEGE YEAH" to the variable PWN. 

## The Solve
To solve the challenge, you must ensure that the entire value, `COLLEGE YEAH`, is treated as a single entity. In the shell, this can be done by using a method to prevent the space from being interpreted as a separator. The solution would be to encapsulate the multi-word string in a way that treats it as a single token, avoiding the shell splitting it up.

code:
```
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{gvC-2y5JgwgVN2etELt_AEKsByw.QXwYTN0wiMwEzNzEzW}
```

## What I learnt 
The key concepts here I learnt are variable assignment and shell parsing. When assigning a value to a variable, there should be no spaces around the `=` sign. Additionally, spaces within a value are interpreted by the shell as argument separators, which can cause errors. 

## References
None used for this challenge


## Exporting Variables
The challenge asks to work with environment variables in the shell. Specifically, it requires setting the variable PWN to the value COLLEGE and exporting it, while setting another variable COLLEGE to the value PWN but not exporting it. After setting up the variables, you must run a command (/challenge/run) where the PWN variable is inherited because it was exported, but the COLLEGE variable is not inherited because it was not exported.

## The Solve
To solve the challenge, we first set the PWN variable to COLLEGE and export it using the export command. This will ensure that the PWN variable is passed into the environment of child processes. Next, you need to set the COLLEGE variable to PWN, but do not export it. Since it is not exported, it won't be inherited by any child processes, such as the /challenge/run command. After setting the variables, run `/challenge/run`, which will result in the `PWN` variable being inherited, but the COLLEGE variable will not be.

code:
```
hacker@variables~exporting-variables:~$ COLLEGE=PWN
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ export PWN=COLLEGE
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
hacker@variables~exporting-variables:~$ /challenge/run
CORRECT!
You have exported PWN=COLLEGE and set, but not exported, COLLEGE=PWN. Great 
job! Here is your flag:
pwn.college{8J7XZJtjwS7RPV7YpTmLyjXgYZh.QXyYTN0wiMwEzNzEzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

## What I learnt 
The key concepts in this challenge I learnt revolve around local shell variables versus environment variables. By default, when you set a variable in the shell, it is a local shell variable, meaning it is only accessible within the current shell process. Child processes (such as new shells or commands) will not inherit local variables. To make a variable available to child processes, you need to export it, turning it into an environment variable. Once exported, the variable can be inherited by any child process, allowing programs or scripts to access it. This is a crucial concept in managing data flow between processes, especially when dealing with sensitive information or configuring the environment for various commands.

In this challenge, we export the `PWN` variable, making it available to child processes like `/challenge/run`, while ensuring that the `COLLEGE` variable is not exported, meaning it won't be passed into the environment of child processes. 

## References
None used for this challenge


## Printing Exporting Variables
The challenge asks to locate the `FLAG` variable by using a method other than `echo`; specifically, it directs you to use the `env` command to print all exported environment variables and then inspect that output to find the `FLAG` entry.

## The Solve
To solve the challenge, run the `printenv FLAG` command

code:
```
hacker@variables~printing-exported-variables:~$ printenv FLAG
pwn.college{klfjOTv0X1_7q3yvFagwwdr45DI.QX4UTN0wiMwEzNzEzW}
```

## What I learnt
Key concepts in this challenge I learnt include understanding that there are multiple ways to read shell variables (for example `echo` and `env`), that `env` displays only exported environment variables.

## References
None used for this challenge


## Sorting Command Output
The challenge asks to capture the output of the `/challenge/run` command into a shell variable named `PWN` so that the variable holds the flag produced by that command rather than just displaying it directly on the terminal.

## The Solve
To solve the challenge we use command substitution to run `/challenge/run` and assign its stdout to the `PWN` variable, which causes the shell to execute the command, capture what it prints, and store that text into `PWN` so you can inspect or use the flag later from the variable.

code:
```
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo "$PWN"
pwn.college{8nbc38e93hhsqz02p07QgUm7w7a.QX1cDN1wiMwEzNzEzW}
```

## What I learnt 
The key concepts I learnt from the challenge include command substitution (which runs a command and stores its output in a variable), the difference between capturing output and just printing it, and the older backtick syntax. The preferred method today is using `$()` because it’s easier to read and allows for nesting commands more easily.

## References
None used for this challenge


## Reading Input
The challenge asks you to use the read command to set the `PWN` variable to the value `COLLEGE`. The read command allows you to capture user input from the standard input and store it in a variable. In this case, you’ll need to use it to capture the string `COLLEGE` and assign it to `PWN`.

## The Solve
To solve the challenge, use the read command to prompt the user for input, store that input in the `PWN` variable, and make sure the value of `COLLEGE` is captured correctly. Once the variable is set, you can verify it by referencing `PWN` to check that the value has been stored correctly.

code:
```
hacker@variables~reading-input:~$ read -p "INPUT :" PWN
INPUT :COLLEGE
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{A0ygtfH97tGvLtMKhgO6ltkfGVe.QX4cTN0wiMwEzNzEzW}
```

## What I learnt 
Key concepts in this challenge I learnt include understanding the `read` command, which takes input from the user and stores it in a variable, and the use of prompts to guide the user. Another important point is the distinction between input (what the user types) and output (what the program prints), as well as how to properly store user input in a variable and use it in subsequent commands.

## References
None used for this challenge


## Reading Files
Put the current contents of the file `/challenge/read_me` into a shell variable named `PWN` with a single command, without starting an extra program just to read the file.

## The Solve
Use the shell builtin `read` and redirect the file into its standard input so `read` assigns the file’s contents directly into `PWN` in one step.
code:
```
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{kd_v4Ve8zoWvSm954wSlwsEJkSn.QXwIDO0wiMwEzNzEzW}
```

## What I learnt 
This exercise reinforces a few important shell fundamentals. First, shell builtins like `read` can operate on redirected standard input (stdin) and assign values directly to the shell environment, which is more efficient than invoking external utilities. Second, input redirection (`<`) lets you feed files into commands without using pipes or extra processes, eliminating the use of `cat`. Third, the distinction between shell builtins and external programs matters for performance and for whether a variable becomes available in the current shell. Finally, because the file changes over time, reading it directly at the moment you run the built-in guarantees you capture the file’s latest contents rather than an earlier snapshot.

## References
None used for this challenge



# Data Manipulation

## Translating Characters
code:
```
hacker@data~translating-characters:~$ /challenge/run | tr 'A-Za-z' 'a-zA-Z'
yOUR CASE-SWAPPED FLAG:
pwn.college{4Gtyft5wFlAytfR2Q9W12N8soUA.01MxEzNxwiMwEzNzEzW}
```


## Deleting Characters
code:
```
hacker@data~deleting-characters:~$ /challenge/run
Your character-stuffed flag:
p%w^%n^%.%c^%o^%l^%le%g^%e^%{^%s%v^%s%Z^%A^%L^N%d^e^u^6^%2%B^%J^%Eg^%O^Lx%s^b%n%5%P^%4%rN^%.^0^%F%Nx^E^%z^%N%x^%wi^M^%w^E%z^N^%z^%Ez^%W%}^%%
hacker@data~deleting-characters:~$ /challenge/run | tr -d '^%'
Your character-stuffed flag:
pwn.college{svsZALNdeu62BJEgOLxsbn5P4rN.0FNxEzNxwiMwEzNzEzW}
```


## Deleting Newlines
code:
```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d '\n'
Your line-split flag: pwn.college{Unybw9_jIEdjGGCx6kxbYoIICVG.0VNxEzNxwiMwEzNzEzW}
```


## Extracting the First Lines with Head
code:
```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{MLZulJ-UAIheGtGe-kINPSLi6xR.0lNxEzNxwiMwEzNzEzW}
```


## Extracting Specific Sections of Text
code:
```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d ' ' -f 2 | tr -d '\n'
pwn.college{cAsXA-oXxEN4kbNdyzCxNadlf7J.01NxEzNxwiMwEzNzEzW}
```


## Sorting Data
code:
```
hacker@data~sorting-data:~$ sort /challenge/flags.txt | tail -n 1
pwn.college{Eb6IFXS4cUMdvGQUgYbWClxwYUi.0FM0MDOxwiMwEzNzEzW}
```
