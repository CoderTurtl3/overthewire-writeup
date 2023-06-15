In this writeup the levels are seperated by a new line and before every level is the level name. Any commands used are perceeded by a $ as in the linux terminal.
The password location is given as a combination of the level goal and my own explaining.
This writeup doesn't contain my research on the topics. This might or might not change in the future wargames.

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
- "find . -size 1033c ! -executable" finds files that are of size 1033 bytes and non executable. Then file with the last command  lists the file types and atlast we pipe the output to grep with keyword ASCII to get the humanreadable files.
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
- Looking at the hexdump we can idetify the latest compression to be gzip since the file starts with 0x1f8b08 which are the beginning bytes of gzip compression.
- First we need to do a reverse hexdump on the hexdumpfile to get the original file.
- This can be done using xxd with "-r" flag
$ xxd -r data.txt >bdata.gz
- And now to decompress the file.
$ gzip -d bdata.gz
- The file is still compressed since the insides are just junk bytes.
- We can take a look at the raw data by doing a hexdump on the new file.
$ xxd bdata >gzuncompressed.txt
- The first bytes are now different (0x425a68) so the file has been compressed using some other compression tool.
- These bytes are the signature bytes of bzip2 file format.
$ mv bdata bdata.bz2
$ bzip2 -d bdata.bz2
- Yet again the data is just some junk so we need to find the next compression tool. The steps to finding the right tool are pretty much the same as before so I won't go as much into the details.
$ xxd bdata >bz2uncompressed.txt
- The first bytes are 0x1f8b08 so it's gzip yet again.
$ mv bdata bdata.gz
$ gzip -d bdata.gz
- Junk...
$ xxd bdata >gzuncompressed2.txt
- The hexdump now has at the start the original filename which to me indicates tar being used.
$ mv bdata bdata.tar
$ tar -xf bdata.tar
- We get a file called "data5.bin" which again is a tar file...
$ mv data5.bin data5.tar
$ tar -xf data5.tar
- Now we have a "data6.bin" file which has some different stuff.
$ xxd data6.bin >taruncompressed.txt
- First bytes 0x425a68 so bzip2.
$ mv data6.bin data6.bz2
$ bzip2 -d data6.bz2
- Tar again
$ mv data6 data6.tar
- File "data8.bin"
$ xxd data8.bin >taruncompressed2.txt
- First bytes 0x1f8b08 so gzip.
$ mv data8.bin data8.gz
$ gzip -d data8.gz
- And finally we get the next password:
"The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw"
- This propably could have been automated but anyways we got the password...

13->14
- Connect to bandit.labs.overthewire.org on port 2220 via SSH as user "bandit13"
$ ssh bandit13@bandit.labs.overthewire.org -p 2220
- The password for bandit14 is stored in "/etc/bandit_pass/bandit14" and can only be read by user bandit14.
- For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.
- The private ssh key is in a file called "sshkey.private" and it can be used with ssh using the flag "-i".
$ ssh -i sshkey.private bandit14@localhost -p 2220
Note: localhost refers to the current machine.

14->15
- You should already be logged in from the last level so check level 13->14 for info on that.
- The password for level 15 can be retrieved by submitting the password of the current level to port 30000 on localhost.
- As stated on level 13-14, the password is in "/etc/bandit_pass/bandit14" and now that we are user bandit14 we can check that.
$ cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
- Now to "submit" the password, we need more information on the port.
- This can be done using a tool called nmap.
$ nmap localhost
- So the port 30000 is used by ndmps.
- nmdps protocol is used for transporting data.
- We can use the tool netcat to communicate with the server.
$ nc localhost 30000
- Now just give the password and press enter. (Use quit to exit nc)
jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

15->16
- The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
- This can be done using openssl.
$ openssl s_client -connect localhost:30001
- After connecting, just give the password we got on the last level.
JQttfApK4SeyHwDlI9SXGR50qclOAil1

16->17
- The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
- Now that we don't have a specific port, we need to scan the range given. This can be done using a port scanner such as nmap.
$ nmap localhost -p 31000-32000
- By just doing a simple scan we find the following ports to be open: 
    31046
    31518
    31691
    31790
    31960
- Since there aren't to many ports we can just test them 1 by 1.
$ openssl s_client -connect localhost:{insert port}
- And after a few tries we got the right port 31790. 


17->18
