# Level 0

## File Navigation

### Solution
```
ls
cat readme
exit
ssh bandit1@bandit.labs.overthewire.org -p 2220
[NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL]
```

### References

[1] Kerrisk, Michael (2023-04-24). [“man7 - Linux manual page”](https://man7.org/linux/man-pages/man1/cat.1.html) Retrieved 2023-10-19.

This helped me understand the usage of the `cat` command which I used to read the value stored in the readme file.

I then SSHed into the bandit labs server with the username `bandit1` with the flag found above as the password.

# Level 1

## Accessing files with dashed names

### Solution
```
ls
cat ./-
exit
ssh bandit2@bandit.labs.overthewire.org -p 2220
[rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi]
```

### References

[1] Raj, Prithvi (2017-02-12). [“stackoverflow - How to open a "-” dashed filename using terminal?](https://stackoverflow.com/questions/42187323/how-to-open-a-dashed-filename-using-terminal) Retrieved 2023-10-20.

When I first used `cat -`, I realised that it `-` was a dashed filename and using `cat -`  would refer to dev/stdin or dev/stdout. Hence, I specified the full location of the file using `./-`

# Level 2

## Accessing files with spaces in their name

### Solution
```
ls
cat "spaces in this filename"
exit
ssh bandit3@bandit.labs.overthewire.org -p 2220
[aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG]
```

### References

I already knew that a whitespace is stored as 20 in Unicode (comes up as %20%) in browser search queries. Therefore, I used a string to mention the filename and turns out that it was the right step!

# Level 3

## Accessing hidden files

### Solution
```
ls
cd inhere
ls -a
cat .hidden
exit
ssh bandit4@bandit.labs.overthewire.org -p 2220
[2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“man7- Linux manual page”](https://man7.org/linux/man-pages/man1/ls.1.html)

On using the conventional "ls", I obviously could not see ".hidden" listed in the directory. Therefore, I referred the cited documentation to use an argument "-a" which evidently lists all the files in the current directory.

# Level 4

## Searching for ASCII text files

### Solution
```
ls
cd inhere
ls -a
file ./-*
cat ./-file07
exit
ssh bandit5@bandit.labs.overthewire.org -p 2220
[lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“man7- Linux manual page”](https://man7.org/linux/man-pages/man1/file.1.html)

The challenge here was finding out the file types of all the files in the `inhere` directory. I refered the cited documentation to find out that that `file` command is used to print the file types of all the files in the location passed as the command parameter
# Level 5

## Search for files matching given parameters

### Solution
```
cd inhere
ls -a
find -size 1033c -type f
cat ./maybehere07/.file2
exit
ssh bandit6@bandit.labs.overthewire.org -p 2220
[P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“man7- Linux manual page”](https://man7.org/linux/man-pages/man1/find.1.html)

I used the documentation cited above to find out that the `-size` and `-type` options can  be used to filter search results arising out of the `find` command. Furthermore, I learnt that the `c` suffix can be added to the size to specify the unit as bytes and that the `f` parameter is used to search for what the documentation termed as "regular files", which seemed like the sanest option and I went for it, obtaining the required flag.

# Level 6

## Search for files with specific owners

### Solution
```
ls -a
find / -user bandit7 -group bandit6 -size 33c
cat /var/lib/dpkg/info/bandit7.password
exit
ssh bandit7@bandit.labs.overthewire.org -p 2220
[z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“man7 - Linux manual page”](https://man7.org/linux/man-pages/man1/find.1.html)

Drawing on the same documentation as the previous level, I leveraged the `find` command with the `-user` and `-group` options in addition to  `-size` which helped me search for files owned by specific users and groups from the question. Also, since the file could be anywhere in the server, I searched from the parent root directory using `/`.

# Level 7

## Search for a word within file

### Solution
```
ls -a
cat data.txt
grep millionth data.txt
exit
ssh bandit8@bandit.labs.overthewire.org -p 2220
[TESKZC0XvTetK0S9xNwm25STk5iWrBvP]
```

### References
[1] Kerrisk, Michael (2023-06-24). [“man7- Linux manual page”](https://man7.org/linux/man-pages/man1/grep.1.html)

I had read about the `grep` for the previous level and figured out that it could be used here instead. Hence, I searched for the word millionth in `data.txt` after being overwhelmed by `cat`ing it and voila, the password was obtained

# Level 8

## Search for unique lines

### Solution
```
ls -a
sort data.txt | uniq -u
exit
ssh bandit9@bandit.labs.overthewire.org -p 2220
[EN632PlfYiZbn3PhVK3XOGSlNInNE00t]
```

### References
[1] Tutorials, Ryan's (2023). ["Linux Tutorials - 11. Piping and Redirection”](https://ryanstutorials.net/linuxtutorial/piping.php)

I used `uniq --help` to learn that option `-u` was to be used but realized that there were several unique lines in the unsorted file, so I decided to sort its content using `sort` and voila!

# Level 9

## Convert non-text files to printable sequences

### Solution
```
ls
strings data.txt | grep "="
exit
ssh bandit10@bandit.labs.overthewire.org -p 2220
[G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s]
```

### References
[1] Linuxopsys (2023-08-15). [“linuxopsys - Strings Command in Linux Explained”](https://linuxopsys.com/topics/strings-command-in-linux)

When I tried to directly `grep` '=', I encountered an error stating "grep: data.txt: binary file matches." When I read 'binary,' I realised that we are dealing with strings here and looked up the cited documentation to read that the `strings` command can be used to extract the namesake from binary sequences.

# Level 10

## Accessing hidden files

### Solution
```
ls
base64 data.txt -d
exit
ssh bandit11@bandit.labs.overthewire.org -p 2220
[6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM]
```

### References
[1] Rainville, Shane (2020-09-01). [“serverlab - How to base64 encode and decode from command-line”](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-base64-encode-and-decode-from-command-line/)

When I intuitively tried `base64 data.txt`, I realised that there must be an option to be used and thus, I learnt about `-decode` from the cited source and used it to decode `data.txt`.

# Level 11

## Accessing hidden files

### Solution
```
ls
cat data.txt |  tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
exit
ssh bandit12@bandit.labs.overthewire.org -p 2220
[JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv]
```

### References
[1] Swenson, Christopher. (2008-03-18). ["Modern Cryptanalysis: Techniques for Advanced Code Breaking"](https://web.archive.org/web/20160624151537/https://books.google.com/books?id=oLoaWgdmFJ8C&pg=PA5)
[2] Ross, Charlie (2018-21-18). [“stackoverflow - using rot13 and tr command for having an encryted email address”](https://stackoverflow.com/a/48897020)

From the [1], I learnt that `ROT13` is a substitution cipher, which I recognized to some degree. I then looked up all the promising ones from commands suggested in the question and learnt that the command `tr` is used to perform text transformations in linux terminals with the `[]` parameters that could be used to specify which characters were to be replaced with what others and thus, specify the `ROT13` algorithm to the `tr` command.


# ---Pulkit Kumar (buddywhitman)