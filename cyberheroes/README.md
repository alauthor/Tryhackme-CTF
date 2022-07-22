# Anonforce | CTF Machine 

## Tools && Sources

1. metasploit

## steps to get two flags 
```bash
[+] open metasploit by writing `msfconsole` in the terminal 
[+] search for http_version 
[+] http is open
[+] in the side menu will will notice login button 
[+] click the login button | will take you to login screen
[+] try to login with any username and a password | a javascript alert will tell you it's not a right username or password 
[+] Ooooh ftp is allowed us to read the whole file system 
[+] it looks we've trying to bypass authentication mechanism 
[+] inspect username element and you will find that the button submeting to a function called `authenticate()` 
[+] open the network tap and click `CTRL + F` to search for `authenticate()`
[+] and the code responsable for authenticate exist in login.html inside a script tag 
[+] username is `h3ck3rBoi` & password reversed `54321@terceSrepuS` so we should reverse it `SuperSecret@12345`
[+] try to login again and you will found the flag | flag   
```
## STEP-1
```bash
msfconsole
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cyberheroes/imgs/1.png">

## STEP-2
```bash
open http://10.10.x.x/login.html
login with any username and password | javascript popup is the result  
inspect username element | you will see that the validation goes to `authenticate()` function 
open network tab and start search for `authenticate()` you will find a function called `authenticate()` inside login.html file  
username is `h3ck3rBoi` but password needs to get reversed from `54321@terceSrepuS` to `SuperSecret@12345`
login and you will get the flag 
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cyberheroes/imgs/2.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/cyberheroes/imgs/3.png">
