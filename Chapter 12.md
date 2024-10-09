# Appendix C: Git Commands

Is kitab mein humne kai Git commands ka zikar kiya hai aur unhein kahani ke taur par introduce karne ki koshish ki hai, jahan hum dheere dheere naye commands ko add karte gaye hain. Lekin is wajah se humare paas commands ka istemal ka kuchh example kitab ke har jagah scattered hai. Is appendix mein, hum un sab Git commands par nazar daalenge jo humne kitab mein discuss kiye hain
it init
Agar aap kisi directory ko ek naya Git repository mein badalna chahte hain, toh aap bas git init run kar sakte hain.

Humne isse Getting a Git Repository mein introduce kiya hai, jahan hum ek naya repository create karte hain.
Remote Branches mein humne is command ka zikar kiya hai jab hum "master" branch ka naam badal rahe hain.

## git clone
git clone command asal mein kai doosri commands ka wrapper hai. Ye ek naya directory create karta hai, usme chala jata hai aur git init run karta hai taaki wo ek khali Git repository ban jaye, remote ko add karta hai (jo default taur par origin hota hai), remote repository se fetch karta hai aur phir latest commit ko aapke working directory mein checkout karta hai.
## Basic Snapshotting
Content ko stage karne aur history mein commit karne ke basic workflow ke liye sirf kuch basic commands hain.

## git add
git add command working directory se content ko staging area (ya "index") mein add karta hai agle commit ke liye. Jab git commit command run hoti hai, by default ye sirf is staging area ko dekhta hai, toh git add ka istemal aapke agle commit snapshot ko tayyar karne ke liye hota hai.

- Ye command bahut hi zaroori hai aur is kitab mein lagbhag har jagah istemal hota hai.
- Isse hum pehli baar Tracking New Files mein introduce karte hain.
- Hum ise Basic Merge Conflicts mein merge conflicts resolve karne ke liye istemal karte hain.
- Interactive Staging mein hum ise sirf specific parts of a modified file ko interactively stage karne ke liye use karte hain.
## git status
git status command aapko aapke working directory aur staging area mein files ki alag alag states dikhata hai. Kaun si files modified hain, unstaged hain aur kaun si staged hain par lekin abhi tak committed nahi hain. Iska normal form kuch basic hints bhi dikhata hai ki kaise files ko in states ke beech move kiya jaye.
## git diff
git diff command ka istemal do trees ke beech differences dekhne ke liye hota hai, jaise working environment aur staging area ke beech.

Basic Use: Staged aur unstaged changes dekhna.
Whitespace Issues: --check option se check karna.
Branch Differences: git diff A…B syntax se compare karna.
Submodule Changes: --submodule option se compare karna.
## git difftool
git difftool ek external tool ko launch karta hai differences dekhne ke liye.

## git commit
git commit command staged files ka snapshot le kar ek new commit banata hai.

## git reset
git reset command undo karne ke liye hota hai, HEAD pointer ko move karta hai aur staging area ko change kar sakta hai.

## git rm
git rm command files ko staging area aur working directory se remove karta hai.

## git mv
git mv command file ko move karta hai aur naye file par git add aur purani file par git rm karta hai.

## git clean
git clean command unwanted files ko working directory se remove karta hai.

## Branching and Merging
git branch command branches ko manage karta hai (list, create, delete, rename).

Tracking Branches: git branch -u se tracking branch setup karna.

