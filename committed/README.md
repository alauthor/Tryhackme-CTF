# commited | CTF Machine 

## Tools && Sources

1. git  
2. [github-desktop](https://desktop.github.com/) (Optional)

## steps to get the flag
```bash
1- using nc I was able to download the file to my own machine 
2- it's easier if you could open the commit on `github desktop app` 
2.1- another manually way to do this 
	1- git branch will display the branches used 
	2- found two branches 
	3- switch to the other branch | git checkout dbint | dbint is the other branch 
	4- display all commits using  | git log
	5- the commit `DB Check` is the one which we are looking for | commit 3a8cc16f919b8ac43651d68dceacbb28ebb9b625
	6- git switch 3a8cc16f919b8ac43651d68dceacbb28ebb9b625   
	7- once you switch | list directory | ls -lh 
	8- cat main.py found | flag-1
```
## STEP-1
```bash
open the github desktop app switch to the other branch and check commits and you will find the flag at `DB check` commit message 
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/committed/imgs/2022-07-10%2002_03_00-.png">

## STEP-1.2
```bash
git branch | will display all branches used in this repo 
git checkout dbint | dbint is the other branch 
git log | will display all commits within the branch dbint 
the commit which we're interested in is 3a8cc16f919b8ac43651d68dceacbb28ebb9b625 `DB Check`
git switch 3a8cc16f919b8ac43651d68dceacbb28ebb9b625 | will switch to that specific commit
cat main.py | Ooooh found | flag-1
```
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/committed/imgs/2022-07-10%2002_25_35-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/committed/imgs/2022-07-10%2002_26_01-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/committed/imgs/2022-07-10%2002_23_54-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
<img src="https://github.com/alauthor/Tryhackme-CTF/blob/main/committed/imgs/2022-07-10%2002_12_30-Kali-Linux-2020.4-vbox-amd64%20(6_18_2022)%20%5BRunning%5D%20-%20Oracle%20VM%20VirtualBox.png">
