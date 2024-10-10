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

