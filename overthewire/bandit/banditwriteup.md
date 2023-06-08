0
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit0"
$ ssh bandit0@bandit.labs.overthewire.org -p 2220
- Login with password "bandit0" as given by the site.

0->1
- The password for bandit1 is in the file "readme"
$ cat readme
NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

1->2
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit1"
$ ssh bandit1@bandit.labs.overthewire.org -p 2220
- The password for bandit2 is in the file "-"
- Since the filename contains a special character we cannot just use "cat -"
- To get the password we can use < symbol after cat to indicate the special filename.
$ cat < -
rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

2->3
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit2"
$ ssh bandit2@bandit.labs.overthewire.org -p 2220
- The password for bandit3 is in the file "spaces in this filename"
- To let cat know we want the one specific file with spaces instead of many different files, we can use "\ "
$ cat spaces\ in\ the\ filename
aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

3->4
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit3"
$ ssh bandit3@bandit.labs.overthewire.org -p 2220
- The password for bandit4 is in a hidden file inside a folder called "inhere"
- To list all files including any hidden, we can use
$ ls -la
- We find out the hidden file is called ".hidden"
$ cat .hidden 
2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

4->5
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit4"
$ ssh bandit4@bandit.labs.overthewire.org -p 2220
- The password for bandit5 is in the only human-readable file in the "inhere" directory.
- Taking a look inside the "inhere" directory we can see 10 files called "-filexx" xx going from 00 to 09.
- To find the human-readable file we can use
$ file -- -file*
- And with that we see the only file containing ASCII text is the file "-file07"
$ cat < -file07
lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

5->6
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit5"
$ ssh bandit5@bandit.labs.overthewire.org -p 2220
- The password for bandit6 is in a file that has the following properties:
    * human-readable
    * 1033 bytes in size
    * not executable
- We can use the following command to find what we want.
$ file `find . -size 1033c ! -executable` | grep ASCII
- "find . -size 1033c ! -executable" finds files that are of size 1033 bytes and non executable. Then file with the last command inside these `` lists the file types and atlast we pipe the output to grep with keyword ASCII to get the humanreadable files.
- the password is in the file "inhere/maybehere07/.file2"
$ cat inhere/maybehere07/.file2
P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

6->7
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit6"
$ ssh bandit6@bandit.labs.overthewire.org -p 2220
- The password for bandit7 is somewhere on the server and has all the following properties:
    * owned by user bandit7
    * owned by group bandit6
    * 33 bytes in size
- The file is somewhere on the server meaning we can backup a few foders until we are at the root dir.
$ cd ../..
$ find -group bandit6 -user bandit7 -size 33c
- The only file we got permission for is "./var/lib/dpkg/info/bandit7.password"
$ cat ./var/lib/dpkg/info/bandit7.password
z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

7->8
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit7"
$ ssh bandit7@bandit.labs.overthewire.org -p 2220
- The password for bandit8 is stored in the file "data.txt" next to the word "millionth"
- To find the password we can pipe the output of cat to grep.
$ cat data.txt | grep millionth
TESKZC0XvTetK0S9xNwm25STk5iWrBvP

8->9
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit8"
$ ssh bandit8@bandit.labs.overthewire.org -p 2220
- The password for bandit9 is stored in the file "data.txt" and is the only line of text that occurs only once.
- We can use "uniq" command but before that the file must be sorted. That is because uniq will only remove repeated lines if they are adjacent to each other.
$ sort data.txt | uniq -u
EN632PlfYiZbn3PhVK3XOGSlNInNE00t

9->10
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit9"
$ ssh bandit9@bandit.labs.overthewire.org -p 2220
- The password for bandit10 is stored in the file "data.txt" in one of the few human-readable strings, preceded by several "=" characters.
- If we just cat the file, we get a big mess of a file so instead we can use "strings" command to get the individual strings.
$ strings data.txt |grep ===
- This gives us the following:
========== the#
========== password
========== is
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

10->11
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit10"
$ ssh bandit10@bandit.labs.overthewire.org -p 2220
- The password for bandit11 is stored in the file "data.txt", which contains base64 encoded data.
- Linux has a tool called "base64" which we can use to decode the data.
$ base64 -d data.txt
The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

11->12
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit11"
$ ssh bandit11@bandit.labs.overthewire.org -p 2220
- The password for bandit12 is stored in the file "data.txt", where all letters have been rotated by 13 positions.
- This is a Rot13 substitution cipher.
- Though it is a simple enough cipher to solve by hand there are tools online to solve it. (I used rot13.com)
The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

12->13
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit12"
$ ssh bandit12@bandit.labs.overthewire.org -p 2220
- The password for bandit13 is stored in the file "data.txt" which is a hexdump of a file that has been repeatedly compressed.
