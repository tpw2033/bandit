## Travis Wright
## Bandit Activity


### Level: 0

Password Found: bandit0

Description: Used ssh to login to the bandit0 server.

```bash
ssh bandit0@bandit.labs.overthewire.org -p2220
```

### Level: 0 -> 1

Password Found: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL

Description: Viewed the readme file to see the password

```bash
cat readme
```

### Level: 1 -> 2

Password Found: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi

Description: Used redirection to view a file with "-" 
as filename.

```bash
ssh bandit1@bandit.labs.overthewire.org -p2220
cat < -
```

### Level: 2 -> 3

Password Found: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG

Description: Used the tab key to autocomplete the filename
for the "space in this filename" 

```bash
ssh bandit2@bandit.labs.overthewire.org -p2220
cat spaces\ in\ this\ filename
```

### Level: 3 -> 4

Password Found: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe

Description: Used "ls -lah" to view hidden files, then
viewed the hidden file using cat.

```bash
ssh bandit3@bandit.labs.overthewire.org -p2220
cd inhere
ls -lah
cat .hidden
```

### Level: 4 -> 5

Password Found: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR

Description: Used cat on the different files until
I found the human-readable file with the password.

```bash
ssh bandit4@bandit.labs.overthewire.org -p2220
cd inhere
cat < -file07
```

### Level: 5 -> 6

Password Found: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

Description: Used recursive ls to view all files in the inhere directory,
then I looked through the list until I found a file that matched the properties 
such as size, human-readable, etc.

```bash
ssh bandit5@bandit.labs.overthewire.org -p2220
ls -lah -R
cd maybehere07
cat .file2
```

### Level: 6 -> 7

Password Found: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S

Description: Used the "find" command to find the file on the server, specifying the 
owner bandit7, group bandit6, and size 33 bytes. Then I used cat to view password.

```bash
ssh bandit6@bandit.labs.overthewire.org -p2220
find / -user bandit7 -group bandit6 -size 33c
cat /var/lib/dpkg/info/bandit7.password
```


### Level: 7 -> 8

Password Found: TESKZC0XvTetK0S9xNwm25STk5iWrBvP

Description: Used the find feature on vim to narrow down the text file to the line 
where password is located.

```bash
ssh bandit7@bandit.labs.overthewire.org -p2220
vim data.txt
/millionth
```

### Level: 8 -> 9

Password Found: EN632PlfYiZbn3PhVK3XOGSlNInNE00t

Description: Used sort to sort lines of text file, then uniq -u to find all unique lines, 
which is the password line.

```bash
ssh bandit8@bandit.labs.overthewire.org -p2220
sort data.txt | uniq -u
```

### Level: 9 -> 10

Password Found: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s

Description: Used the strings command on the text file to show all human-readable strings,
and then found password by looking for = characters in the output list.

```bash
ssh bandit9@bandit.labs.overthewire.org -p2220
strings data.txt
```

### Level: 10 - > 11

Password Found: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM

Description: Used the base64 with decode flag to decode the base64 encoded text file,
which reveals the password.

```bash
ssh bandit10@bandit.labs.overthewire.org -p2220
base64 -d data.txt
```

### Level: 11 -> 12

Password Found: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

Description: Used the tr translate command to rotate all letters 13 positions again,
restoring the original file with password. 

```bash
ssh bandit11@bandit.labs.overthewire.org -p2220
cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

### Level: 12 -> 13

Password Found: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw

Description: ...

```bash
mkdir /tmp/travis123
cp data.txt /tmp/travis123
cd /tmp/travis123
cat data.txt
xxd -r data.txt > hexdump
file hexdump
mv hexdump hexdump.gz
gzip -d hexdump
xxd hexdump
mv hexdump hexdump.bz2
bzip2 -d hexdump.bz2
mv hexdump hexdump.gz
gzip -d hexdump.gz
xxd hexdump
xxd data5.bin
tar -xf data5.bin
mv data5.bin data5.tar
tar -xf data5.tar
xxd data6.bin
bzip2 -d data6.bin
xxd data6.bin.out
mv data6.bin.out data6.tar
tar -xf data6.tar
xxd data8.bin | head
mv data8.bin data8.gz
gzip -d data8.gz
cat data8
```

### Level: 13 -> 14

Password Found: SSH Key

Description: To log in to the next level, I used cat on the sshkey present, then I just copied the contents
to a local file on my PC to login with.

```bash
ssh bandit13@bandit.labs.overthewire.org -p2220
ls
cat sshkey.private
```

### Level: 14 -> 15

Password Found: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt

Description: Once logged in with the sshkey from the last level, I looked in 
the password directory to find the password of this level. Then, I connected to localhost on 30000
using netcat, and input the password, which then returned me the password for the next level.

```bash
ssh -i .\sshkey.private bandit14@bandit.labs.overthewire.org -p2220
cat /etc/bandit_pass/bandit14
fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq
nc localhost 30000
```

### Level: 15 -> 16

Password Found: JQttfApK4SeyHwDlI9SXGR50qclOAil1

Description: I used openssl to connect as client to localhost on 30001 and submit the 
password of the current level, and then I receive the password for the next level.

```bash
ssh bandit15@bandit.labs.overthewire.org -p2220
openssl s_client -connect localhost:30001
```

### Level: 16 -> 17

Password Found: SSH Key

Description: I use nmap with the -sV to search all port services on localhost between
31000 and 32000. From there I saw 2 SSL ports, 31518 and 31790, which I tested to connect to with
openssl. 31518 just returned the value, but 31790 correctly returned the next level's SSH key.

```bash
ssh bandit16@bandit.labs.overthewire.org -p2220
nmap -sV localhost -p 31000-32000
openssl s_client -connect localhost:31518
openssl s_client -connect localhost:31790
```

### Level: 17 -> 18

Password Found: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg

Description: Since there are 2 passwords files with 1 line changed, I used the diff 
command to find the differing line, which is the password for the next level.


```bash
ssh -i .\sshkey.private bandit17@bandit.labs.overthewire.org -p2220
diff passwords.old passwords.new
```

### Level: 18 -> 19

Password Found: awhqfNnAbc1naukrpqDYcF95h7HoMTrC

Description: Since someone modified .bashrc to log out upon login, I appended the commands 
to the SSH connection to see the files, and view the readme file in the home directory, which
contained the next level password.

```bash
ssh bandit18@bandit.labs.overthewire.org -p2220
ssh bandit18@bandit.labs.overthewire.org -p2220 ls
ssh bandit18@bandit.labs.overthewire.org -p2220 cat readme
```

### Level: 19 -> 20

Password Found: VxCazJaVykI6W36BkBU0mJTCM8rR95XT

Description: I first ran the setuid binary to see the usage, which runs a command as
bandit20. I then ran cat to see the password for the next level, since it is only
accessible as bandit20.

```bash
ssh bandit19@bandit.labs.overthewire.org -p2220
ls
./bandit20-do
./bandit20-do cat /etc/bandit_pass/bandit20
```

### Level: 20 -> 21

Password Found: NvEJF7oVjkddltPSrdKEFOllh9V1IBcq

Description: There is a different setuid binary in this directory that connects to 
a localhost port, reads a line, and if valid, displays the next level's password. To accomplish this,
I send the level password with echo -n to avoid newline, and pipe the result into netcat, listening on 
port 1234, running in the background so that I can then use suconnect on 1234, which displays the next level's
password.

```bash
ssh bandit20@bandit.labs.overthewire.org -p2220
ls
./suconnect
echo -n "VxCazJaVykI6W36BkBU0mJTCM8rR95XT" | nc -l -p 1234 &
./suconnect 1234
```

