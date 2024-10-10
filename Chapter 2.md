# Git Basics
.git directory woh folder hai jo Git repository ke andar hota hai. Ismein sabhi necessary files hoti hain jo Git ko version control karne ke liye chahiye hoti hain. Yeh files project ke history aur versioning ko manage karti hain.
## Cloning an Existing Repository
Agar aap  kisi existing Git repository ka copy chahte hain, toh aap git clone command ka use karte hain. Ismein aapko sirf ek working copy nahi milti, balki project ki saari versions aur history bhi milti hai.

Cloning Ka Example
```
$ git clone https://github.com/libgit2/libgit2
```
Is command se ek directory libgit2 create hoti hai, jo saare repository ka data aur latest version ko check out karti hai.

Agar aap kisi aur naam ki directory mein clone karna chahte hain, toh aap yeh command use kar sakte hain:
```
$ git clone https://github.com/libgit2/libgit2 mylibgit
```
##  Git Repository Kaise Banta Hai?
Aapko Git repository hasil karne ke liye do tarike hote hain:

Aap kisi local directory ko Git repository mein convert kar sakte hain.
Aap kisi existing repository ko clone kar sakte hain.
Existing Directory Mein Repository Initialize Karna
Agar aapke paas koi project directory hai jo abhi version control mein nahi hai, toh pehle us directory mein jayein. Commands yeh hain:

Linux:
```
$ cd /home/user/my_project
```
Ab yeh command type karein:
```
$ git init
```
Yeh ek .git naam ka subdirectory banata hai jismein aapki repository files hoti hain. Is stage par koi bhi project file track nahi hoti.
## Existing Files Ko Version Control Karna
Agar aap existing files ko version control shuru karna chahte hain (khali directory ke bajaye), toh aapko pehle un files ko track karna hoga aur initial commit karna hoga. Iske liye aap yeh commands use kar sakte hain:
```
$ git add *.c
$ git add LICENSE
$ git commit -m 'Initial project version'
```
git add command se aap specify karte hain ki kaunse files ko aap track karna chahte hain.
git commit command se aap changes ko repository mein commit karte hain.
Is point par, aapke paas ek Git repository hai jismein tracked files hain aur ek initial commit ho chuka hai.
![gitt](https://github.com/user-attachments/assets/2bcc5bb8-c4e0-469b-bc05-c5401f926aef)

## Checking the Status of Your Files
Jab aapko yeh jaanana ho ki aapki files kis state mein hain, toh aap git status command ka istemal karte hain. Agar aap yeh command ek clone karne ke baad chalayenge, toh aapko kuch aisa output dekhne ko milega:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```
Iska matlab hai ki aapka working directory clean hai; yani ki aapki koi bhi tracked files modified nahi hain. Git ko koi untracked files bhi nahi dikhai deti, warna yeh yahan listed hoti. Aakhir mein, yeh command aapko batata hai ki aap kis branch par hain 
## Staging Modified Files in Git
Jab aap apne project mein ek naya file add karte hain, jaise ki ek simple README file, toh aapko yeh samajhna hoga ki Git kaise is file ko track karta hai. Chaliye is process ko samjhte hain:

1. Naya File Banana
Maan lijiye aap ek README file create karte hain:
```
$ echo 'My Project' > README
```
2. git status Command Chalana
Ab agar aap git status command chalate hain, toh aapko kuch is tarah ka output milega:

vbnet
Copy code
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README

nothing added to commit but untracked files present (use "git add" to track)
Is output mein "Untracked files" ka section dikha raha hai. Matlab, Git ne dekha ki aapke last snapshot (commit) mein yeh file nahi thi, aur yeh abhi tak staged nahi hui hai. Git is file ko commit snapshots mein include nahi karega jab tak aap isay explicitly nahi batate.

3. Naye Files Ko Track Karna
Agar aap chahte hain ki README file track ho jaye, toh aapko git add command use karni hogi:

bash
Copy code
$ git add README
4. Phir Se git status Chalana
Ab agar aap phir se git status command chalate hain, toh output kuch is tarah hoga:

vbnet
Copy code
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
    new file:   README
Yahan aap dekh sakte hain ki aapki README file ab "Changes to be committed" section mein hai. Matlab, yeh staged hai, aur agar aap is point par commit karte hain, toh is file ka jo version aapne git add ke waqt banaya tha, wahi aapke agle historical snapshot mein save ho jayega.
