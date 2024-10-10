# GIT
Yahaan aapko Git ke baare mein chapter-by-chapter samjhaaya jaayega. Har chapter Git ke kisi na kisi important concept ko simple aur easy language mein explain karega.
# Getting Started 
Yeh chapter Git ke saath shuru karne ke baare mein hoga. Hum pehle version control tools ke background ke baare mein samjhenge, phir Git ko apne system par kaise install karna hai, aur kaise kaam shuru karne ke liye setup karna hai. Is chapter ke ant mein aap samajh jayenge ki Git kyun zaroori hai, aapko isse kyun use karna chahiye, aur aap ready honge isse istemal karne ke liye.

Version Control ke baare mein Version control kya hota hai aur aapko iski zaroorat kyun hai? Version control ek aisi system hai jo kisi file ya file set par samay ke saath hone wale changes ko record karta hai, taaki aap specific versions ko baad mein recall kar sakein. Iss book ke examples mein hum software source code ka use karenge, lekin aap computer par kisi bhi type ki file ka version control kar sakte hain.

Agar aap ek graphic ya web designer hain aur aapko kisi image ya layout ke sabhi versions ko save karna hai, toh Version Control System (VCS) ka istemal ek wise choice hai. Yeh aapko files ko pichle state mein revert karne, puri project ko wapas pichle state mein lane, changes ko samay ke saath compare karne, aur kisne kya modify kiya yeh dekhne mein madad karta hai. VCS use karne ka ek aur fayda yeh hai ki agar kuch galat ho jaye ya files kho jayein, toh aap asani se recover kar sakte hain.

## Local Version Control Systems
Bohot log files ko alag directory mein copy kar ke version control karte hain, lekin yeh method galtiyon se bhara hota hai. Is issue ko solve karne ke liye, local VCS develop kiye gaye jo ek simple database mein files ke changes ko record karte hain.

## Centralized Version Control Systems (CVCS)
Jab logo ko different systems par kaam karte hue collaborate karna hota hai, toh Centralized Version Control Systems ka istemal kiya jata hai. CVCS ek central server par sabhi versioned files ko rakhta hai aur users files ko wahaan se check out karte hain. Lekin iska ek major drawback yeh hai ki agar server fail ho jaye, toh pura project history kho sakte hain.
![vcs](https://github.com/user-attachments/assets/5e0e8dda-c5d7-4a66-a9a1-e46269f5120e)


## Distributed Version Control Systems (DVCS)
Distributed Version Control Systems (jaise Git, Mercurial) mein har client ke paas repository ka full history hota hai. Agar koi server fail ho jaye, toh client repositories se data recover kiya ja sakta hai. Is system mein aap simultaneously alag-alag groups ke saath kaam kar sakte hain aur hierarchical workflows bhi set kar sakte hain jo centralized systems mein possible nahi hote.

## Git ki Short History
Git ka shuruat ek controversy ke saath hui. Linux kernel ek open source software project hai. 1991 se 2002 tak, changes patches aur archived files ke roop mein distribute kiye jate the. 2002 mein Linux kernel project ne BitKeeper naam ka proprietary DVCS use karna shuru kiya. 2005 mein BitKeeper ka free status khatam ho gaya aur Linus Torvalds ne apna tool banaya jisse Git ka janm hua. Git ka goal tha speed, simple design, non-linear development, aur distributed system ko support karna.Git Mein Integrity Hoti Hai
Git mein har file checksummed hoti hai aur usse uske unique SHA-1 hash ke through store kiya jaata hai. Is wajah se, bina Git ko pata chale, koi file badli nahi ja sakti. Hash se files ka tracking hota hai, jo integrity maintain karta hai.

2005 ke baad se, Git evolve aur mature hua hai, lekin apne initial qualities ko retain kiya hai. Yeh bohot fast hai, large projects ke liye efficient hai, aur branching system bohot strong hai
## Git kya hai:
Git ek Version Control System (VCS) hai jo files ka record rakhta hai aur unke changes ko track karta hai. Yeh doosre VCSs jaise CVS, Subversion, ya Perforce se alag hai kyunki Git information ko ek unique tarike se store karta hai. Isliye, agar aap Git seekhte waqt purane systems ke concepts ko hata kar samjhenge, toh aapko confusion kam hoga aur Git ko effectively use karna aasan hoga
# Git Mein Integrity Hoti Hai
Git mein har file checksummed hoti hai aur usse uske unique SHA-1 hash ke through store kiya jaata hai. Is wajah se, bina Git ko pata chale, koi file badli nahi ja sakti. Hash se files ka tracking hoti hai, jo integrity maintain karta hai.
The Three States (Hinglish mein):

Git mein aapke files teen main states mein ho sakti hain: modified, staged, aur committed:

- Modified: Jab aapne file ko change kiya hai lekin abhi tak commit nahi kiya.
- Staged: Aapne modified file ko next commit ke liye mark kiya hai.
- Committed: Data aapke local database mein safely store ho gaya hai.
## The Command Line

Git ko use karne ke bahut tareeke hain. Ek hai original command-line tools ka istemal, aur doosra graphical user interfaces (GUIs) ka use karna. Is book mein hum command line pe Git ka use karenge. Command line pe aap saare Git commands run kar sakte ho, jabki GUIs mein sirf limited functionalities hoti hain. 
Ubuntu mein Git install karne ke liye, aapko terminal ka istemal karna hoga. Neeche diye gaye steps ko follow karein:
## Installing Git
Terminal kholein: Sabse pehle apna terminal open karein.

Package list update karein: Latest package information ko update karne ke liye yeh command chalayein:
```
sudo apt update
```
Git install karein: Ab Git install karne ke liye yeh command type karein:
```
sudo apt install git-all
```
Installation confirm karein: Install hone ke baad yeh command chalakar check karein ki Git sahi se install ho gaya hai ya nahi:
```
git --version
```
Agar aapko Git ka version show ho jaye, to iska matlab Git successfully install ho gaya hai.

Ab aap Git commands use karne ke liye ready hain!
## First-Time Git Setup
Ab jab tumhare system par Git install ho gaya hai, toh kuch cheezein customize karna zaroori hai apne Git environment ke liye. Yeh cheezein tumhe sirf ek baar har computer par karni hongi, aur yeh settings upgrades ke beech bhi rahengi. Tum inhe kabhi bhi change kar sakte ho dobara commands run karke.

Git ke saath ek tool aata hai jiska naam hai git config, jo tumhe configuration variables set karne aur dekhne mein madad karta hai.
```
git config --list --show-origin
```
## Your Identity
Jab tum Git install karte ho, pehli cheez jo tumhe karni chahiye, woh hai apna user name aur email address set karna. Yeh zaroori hai kyunki har Git commit yeh information use karta hai, aur yeh commit ke andar permanently save ho jaata hai.

Command use karne ka tareeqa:
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
## Your Editor
Ab jab tumhara identity set ho gaya hai, tum apne default text editor ko bhi configure kar sakte ho, jo Git tab use karega jab tumhe ek message type karna padega. Agar tumne kuch configure nahi kiya, toh Git tumhare system ka default editor use karega.

Agar tum koi doosra text editor use karna chahte ho, jaise Emacs, toh tum yeh command use kar sakte ho:
```
$ git config --global core.editor emacs
```
## Your Default Branch Name
By default, Git ek naya repository banate waqt "master" branch banata hai jab tum git init command use karte ho. Lekin, Git version 2.28 se onwards, tum initial branch ka naam customize kar sakte ho.

Agar tum chahte ho ki initial branch ka naam main ho, toh yeh command use kar sakte ho:
```
$ git config --global init.defaultBranch main
```
Isse tumhare naye repositories ka default branch name "main" ban jayega
Yeh command tumhare Git ke liye Emacs ko default editor bana degi.

## Checking Your Settings
Agar tum apne Git configuration settings check karna chahte ho, toh tum git config --list command use kar sakte ho. Is command se tumhe Git ke saare settings dikhenge jo us waqt Git ko mile hain:
```
$ git config --list
user.name=John Doe  
user.email=johndoe@example.com  
color.status=auto  
color.branch=auto  
color.interactive=auto  
color.diff=auto  
...
```
Kabhi kabhi tumhe same key multiple times dikh sakti hai, kyunki Git same key ko alag files se padh sakta hai (jaise [path]/etc/gitconfig aur ~/.gitconfig). Aise cases mein Git hamesha last value ko use karega jo usse milegi.

Agar tumhe kisi specific key ka value dekhna hai, toh yeh command use kar sakte ho:
```
$ git config user.name
John Doe
```
## Getting Help with Git in Hinglish
Agar aapko Git use karte waqt madad ki zaroorat hai, to aap Git commands ke liye comprehensive manual page (manpage) help teen tarikon se le sakte hain:
```
$ git help <verb>
```
Is command se aap specific Git command ka help dekh sakte hain. Jaise, agar aapko git config ke baare mein jaana hai, to aap likhenge:
```
$ git help config
$ git <verb> --help
```
Is tarike se bhi aap help le sakte hain. Ye bhi wahi information dega.
```
$ man git-<verb>
```
Ye command bhi help provide karega, lekin manpages format mein.
## Quick Help
Agar aapko sirf Git command ke options ya syntax ka quick refresher chahiye, to aap -h option use karke help output le sakte hain. Jaise:
```
$ git add -h
```
## The Three States
Dhyaan se suno— yeh Git ka sabse important point hai agar tum apni learning process ko smoothly chalana chahte ho. Git mein tumhare files teen main states mein ho sakte hain: modified, staged, aur committed:

- Modified: Matlab tumne file mein changes kiye hain, par ab tak usse apne database mein commit nahi kiya hai.
- Staged: Matlab tumne ek modified file ko mark kar diya hai taki wo tumhare next commit snapshot mein jaaye.
- Committed: Matlab file ka data safely tumhare local database mein store ho gaya hai.
