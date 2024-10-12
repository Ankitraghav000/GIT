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
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
    README
```
nothing added to commit but untracked files present (use "git add" to track)
Is output mein "Untracked files" ka section dikha raha hai. Matlab, Git ne dekha ki aapke last snapshot (commit) mein yeh file nahi thi, aur yeh abhi tak staged nahi hui hai. Git is file ko commit snapshots mein include nahi karega jab tak aap isay explicitly nahi batate.

3. Naye Files Ko Track Karna
Agar aap chahte hain ki README file track ho jaye, toh aapko git add command use karni hogi:
```
$ git add README
```
4. Phir Se git status Chalana
Ab agar aap phir se git status command chalate hain, toh output kuch is tarah hoga:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
```
Changes to be committed:
```
  (use "git restore --staged <file>..." to unstage)
    new file:   README
```
Yahan aap dekh sakte hain ki aapki README file ab "Changes to be committed" section mein hai. Matlab, yeh staged hai, aur agar aap is point par commit karte hain, toh is file ka jo version aapne git add ke waqt banaya tha, wahi aapke agle historical snapshot mein save ho jayega.
## Staging Modified Files
Jab aap ek file ko modify karte hain jo pehle se hi tracked hai, toh Git kaise react karta hai, yeh samajhna zaroori hai. Chaliye, ek example se samjhte hain:

1. Tracked File Ko Modify Karna
Maan lijiye, aap ek pehle se tracked file, jaise ki CONTRIBUTING.md, ko modify karte hain. Iske baad jab aap git status command chalate hain, toh aapko kuch is tarah ka output milega:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    new file:   README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   CONTRIBUTING.md
```
Yahan dekhiye ki CONTRIBUTING.md file "Changes not staged for commit" section mein aa rahi hai. Matlab yeh file tracked thi aur ab modified ho gayi hai, lekin abhi tak staged nahi hui hai. Aapko isay commit mein add karne ke liye git add command chalani hogi.

2. Staging File Using git add
Agar aap git add CONTRIBUTING.md command chalate hain, toh file stage ho jayegi:
```
$ git add CONTRIBUTING.md
```
Ab git status chalane par yeh output aayega:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    new file:   README
    modified:   CONTRIBUTING.md
```
Ab dono files (README aur CONTRIBUTING.md) staged hain aur agle commit mein jaane ke liye ready hain.

3. Dubara File Modify Karna
Maan lijiye aapko CONTRIBUTING.md mein aur ek chhoti si change karni hai, toh aap file ko edit karte hain:
```
$ vim CONTRIBUTING.md
```
Phir git status chalate hain:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    new file:   README
    modified:   CONTRIBUTING.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
    modified:   CONTRIBUTING.md
```
Yahan CONTRIBUTING.md staged aur unstaged dono sections mein dikh raha hai. Yeh isliye hota hai kyunki jab aapne pehli baar git add chalaya tha, tab Git ne file ka us waqt ka version stage kiya tha. Lekin aapne baad mein file modify ki, lekin naye changes staged nahi hain.

4. Latest Changes Ko Stage Karna
Agar aap naye changes ko commit mein include karna chahte hain, toh aapko fir se git add chalana hoga:
```
$ git add CONTRIBUTING.md
```
Ab git status chalane par aapko yeh dikhega:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    new file:   README
    modified:   CONTRIBUTING.md
```
Ab CONTRIBUTING.md ka latest version staged ho gaya hai aur aapka commit ready hai
## Short Status 
1. Short Status ka Use
Agar aap git status output ko chhota  dekhna chahte hain, toh git status -s ya git status --short ka use kar sakte hain. Yeh aapko ek simplified output deta hai jo kaafi compact hota hai. Example ke liye:
```
$ git status -s
 M  README
MM  Rakefile
A   lib/git.rb
 M  lib/simplegit.rb
??  LICENSE.txt
```
Isme symbols ka matlab:

?? ka matlab hai file abhi untracked hai.
A ka matlab file ko stage kar diya gaya hai.
M ka matlab file ko modify kiya gaya hai.
Agar ek file MM dikhti hai, iska matlab hai ki file staged bhi hai aur working directory mein modify bhi ho chuki hai.
## Git Mein Files Ko Ignore Karna 
Kai baar aapke project mein kuch aise files hoti hain jo aap Git mein na toh track karna chahte hain aur na hi Git aapko unhe untracked files ke roop mein dikhaye. Ye files usually automatically generated hoti hain jaise log files, build system ke dwara banayi gayi files, etc. Aise cases mein, aap ek file bana sakte hain jisme un files ke patterns likhe ho jo ignore karne hain, is file ka naam hota hai .gitignore.

Example .gitignore File:
```
$ cat .gitignore
*.[oa]
*~
```
Pehli line Git ko ye batati hai ki kisi bhi .o ya .a extension wali files ko ignore karein. Ye generally build process ke dauran banti hain.
Dusri line batati hai ki Git sabhi files ko ignore karein jinke naam ke aakhri mein tilde (~) symbol ho. Kai text editors, jaise ki Emacs, temporary files ke liye ye symbol use karte hain.
Aap aur bhi directories jaise log, tmp, pid, ya automatically generated documentation files ko ignore kar sakte hain. Apne naye repository ke liye .gitignore file ko shuru mein hi set up kar lena achha hota hai, taaki accidentally aap unwanted files ko Git mein commit na kar dein.

#### .gitignore File Ke Rules:
- Blank lines ya # se shuru hone wali lines ko ignore kiya jata hai.
- Standard glob patterns ka use hota hai aur ye recursively pure working tree mein apply hote hain.
- Aap forward slash (/) ka use** karke recursivity ko avoid kar sakte hain.
- Patterns ke end mein forward slash (/) dal kar directory specify kar sakte hain.
- Aap exclamation point (!) se pattern ko negate kar sakte hain.
#### Glob Patterns:
Glob patterns simplified regular expressions jaisa kaam karte hain. Jaise:

- Asterisk (*) zero ya zyada characters match karta hai.
- [abc] brackets ke andar wale characters ko match karta hai (is case mein a, b, ya c).
- Question mark (?) ek single character ko match karta hai.
- [0-9] 0 se lekar 9 tak ke characters ko match karega.
.gitignore ke Rules
### Blank Lines aur Comments:
Agar file mein koi khaali line ho ya line # se shuru hoti ho, toh Git usse ignore karta hai. Comments likhne ke liye # ka use hota hai.

Example:
```
# Ye comment hai, ise Git nahi padhega
```
- Glob Patterns Ka Use:
Patterns ka matlab hai ki kaunse files ya directories ko ignore karna hai. Ye patterns simplified regular expressions jaisa kaam karte hain. Har pattern recursively pura project folder mein check hota hai.

- Forward Slash (/) Ka Use:
Agar aap pattern ke shuru mein / use karte ho, toh ye batata hai ki ye pattern sirf current directory ke liye valid hai, aage ke subdirectories ke liye nahi.

- Negation (!):
Agar aap kisi pattern ko ignore karte ho, lekin kuch specific files ko ignore nahi karna chahte, toh aap pattern ke shuru mein ! use kar sakte ho. Iska matlab hai, "is pattern ko ignore mat karo."

### Glob Patterns Simplified
Asterisk (*): Ye kisi bhi character ke zero ya zyada group ko match karta hai.

Example:
```
*.log
```
Iska matlab hai sabhi .log files ko ignore karo, jaise error.log, debug.log, etc.

[abc]: Iska matlab hai bracket ke andar jo bhi character ho, unhe match karo.

Example:
```
*.[oa]
```
Iska matlab hai sabhi .o ya .a extension wali files ko ignore karo.

Question Mark (?): Ye ek single character ko match karta hai.

Example:
```
?.txt
```
Iska matlab hai sabhi files jinke naam mein ek character hai aur extension .txt hai, jaise a.txt, b.txt, etc.

[0-9]: Iska matlab hai brackets ke andar diye gaye range ke character ko match karo.

Example:
```
file[1-9].txt
```
Iska matlab hai file1.txt, file2.txt se lekar file9.txt tak ko ignore karo.

Double Asterisk ()**: Ye nested directories ko match karta hai.

Example:
```
**/backup/*.txt
```
Iska matlab hai kisi bhi directory ke andar backup/ folder ho aur usme sabhi .txt files ko ignore karo, chahe wo kitni bhi depth mein ho.

Ek Example .gitignore:
```
# Sabhi .log files ko ignore karo
*.log

# Sirf root directory ka TODO file ignore karo, lekin subdirectories ka nahi
/TODO

# Sabhi build directories aur unke andar ki files ko ignore karo
build/

# doc/notes.txt ko ignore karo, lekin doc/server ke files ko nahi
doc/*.txt

# Sabhi .pdf files ko ignore karo jo doc/ aur uske subdirectories mein ho
doc/**/*.pdf
```
Is example se aap .gitignore ka structure aur patterns samajh sakte ho.

## Staged aur Unstaged Changes dekhna
Agar git status command aapko zyada detail mein nahi bata raha, aur aap yeh jaan'na chahte hain ki aapne kaunse exact lines change ki hain, toh aap git diff command ka use kar sakte hain. Isse aap do bade sawalon ke jawaab jaan sakte hain:

1. Aapne kya change kiya hai jo abhi tak stage nahi hua hai? (yaani aapne git add nahi kiya)
 2. Aapne kya stage kiya hai jo ab commit hone waala hai?

 Agar aap git status chalate ho, toh yeh aapko sirf file names bata deta hai, lekin git diff aapko exact lines dikhata hai jo add ya remove hui hain.
### Example:
Maan lo, aapne README file ko edit aur stage kiya, aur uske baad CONTRIBUTING.md ko edit kiya lekin stage nahi kiya. Aap agar git status chalate ho, toh kuch aisa output milega:
```
$ git status  
On branch master  
Your branch is up-to-date with 'origin/master'.  

Changes to be committed:  
  (use "git reset HEAD <file>..." to unstage)  
  modified:   README  

Changes not staged for commit:  
  (use "git add <file>..." to update what will be committed)  
  (use "git checkout -- <file>..." to discard changes in working directory)  
  modified:   CONTRIBUTING.md
```
### Unstaged Changes Dekhna:
Agar aap yeh dekhna chahte ho ki aapne kya change kiya hai jo abhi tak stage nahi hua, toh aap git diff command use kar sakte ho:

```
$ git diff
```
Is command se aapko working directory ke changes dikhai denge jo abhi tak staging area mein nahi hain.

### Staged Changes Dekhna:
Agar aapko yeh dekhna hai ki aapne kya stage kiya hai jo aapke next commit mein jayega, toh aap git diff --staged ya git diff --cached use kar sakte ho. Dono commands ka kaam ek hi hai:

```
$ git diff --staged
```
Is command se wo changes dikhai denge jo aapne stage kar diye hain aur jo next commit mein add honge.

Example: Mixed Changes (Staged + Unstaged)
Maan lo aapne CONTRIBUTING.md file ko stage kiya, aur phir usme thoda aur edit kiya. Is situation mein, aap git diff aur git diff --cached dono use kar ke dekh sakte ho ki kya staged hai aur kya unstaged hai:
```
$ git add CONTRIBUTING.md  
$ echo '# test line' >> CONTRIBUTING.md  
$ git status
```
Iske baad, agar aap git diff chalate ho toh unstaged changes dikhenge:
```
$ git diff
```
Aur agar aap git diff --cached chalate ho, toh staged changes dikhai denge:
```
$ git diff --cached
```
## Committing Your Changes

Ab tumhara staging area bilkul waise hi set ho gaya hai jaise tumhe chahiye tha, to ab tum apne changes ko commit kar sakte ho. Dhyan rahe, agar koi file unstaged hai — matlab tumne koi file banayi ya modify ki hai par ab tak git add nahi kiya — to wo commit mein nahi aayegi. Wo bas modified file ke roop mein disk par reh jayegi. For example, agar tum git status chalao aur sab kuch staged ho gaya ho, to tum apne changes commit karne ke liye ready ho. Sabse simple way to commit is:
```
$ git commit
```
Isse tumhara editor khulega, jo tumhare shell ke EDITOR environment variable ke according set hota hai (zyadatar vim ya emacs hota hai, par tum ise git config --global core.editor command se apni pasand ka editor set kar sakte ho).

Editor kuch aise dikhega (yaha Vim screen ka example hai):

```
# Please enter the commit message for your changes. Lines starting 
# with '#' will be ignored, and an empty message aborts the commit. 
# On branch master 
# Your branch is up-to-date with 'origin/master'. 
# 
# Changes to be committed: 
#   new file:   README 
#   modified:   CONTRIBUTING.md
```
Tum dekhoge ki yeh default commit message mein git status ka latest output commented out hai, aur ek khaali line upar hai. Tum in comments ko hata ke apna commit message likh sakte ho, ya fir inhe waise hi chod sakte ho, taki yaad rahe ki tum kya commit kar rahe ho.

Aur zyada clarity ke liye, tum git commit ke saath -v option use kar sakte ho, jisse tumhare editor mein diff bhi show ho jayega, taki tum clearly dekh pao ki kya commit kar rahe ho.

Jab tum editor se bahar aate ho, Git tumhare commit message ke saath commit bana deta hai (comments aur diff ko hata ke).

Alternatively, tum inline commit message bhi daal sakte ho -m flag ke saath:
```
$ git commit -m "Story 182: fix benchmarks for speed"
```
Tumhara commit kuch aise dikhega:
```
[master 463dc4f] Story 182: fix benchmarks for speed  
2 files changed, 2 insertions(+)  
create mode 100644 README
```
Isse tumne apna pehla commit bana liya! Tum dekh sakte ho ki commit ne tumhe thoda output diya, jisme branch ka naam, commit ka SHA-1 checksum, kitni files badli gayi, aur lines added ya removed ka stats diya gaya hai.

Yeh commit tumhare staging area ka snapshot record karta hai. Agar tumhe kuch aur changes stage karne hain, tum dusra commit kar sakte ho, taki history mein add ho jaye.

#### Staging Area Skip Karna
Agar tumhe staging area ka process thoda zyada complex lag raha hai, to tum directly -a option ke saath commit kar sakte ho, jisse Git automatically sab tracked files ko stage kar dega. Is tarah tumhe git add command nahi chalani padegi:
```
$ git commit -a -m 'Add new benchmarks'
```
Iss command ka output kuch aise dikhega:
```
[master 83e38c7] Add new benchmarks  
1 file changed, 5 insertions(+), 0 deletions(-)
```
Yaha tumhe git add chalane ki zarurat nahi padi, kyunki -a flag ne sab changed files ko include kar liya. Lekin dhyan se use karna, kyunki kabhi kabhi unwanted changes bhi commit ho jate hain isse.
 Agar aapko apne changes ka detailed view chahiye, toh aap -v option use kar sakte hain:

```
$ git commit -v
```
Jab aap editor se bahar aayenge, Git aapke message ke sath commit create karega. Alternately, aap commit message inline bhi de sakte hain -m flag ke sath:
```
$ git commit -m "Story 182: fix benchmarks for speed"
```
Is command ka output aapko commit ke bare mein batata hai, jaise branch, SHA-1 checksum, files changed, aur lines added ya removed.

Staging Area Ko Skip Karna
Agar aap staging area ko skip karna chahte hain, toh Git iske liye ek simple shortcut provide karta hai. -a option add karke aap git commit command ke sath, Git automatically tracked files ko stage karta hai:
```
$ git commit -a -m 'Add new benchmarks'
```
Is approach se modified files automatically stage ho jaati hain, lekin dhyan rakhein, kyunki isse unwanted changes bhi commit ho sakte hain.

Files Ko Remove Karna
Git se file remove karne ke liye, aapko git rm command ka use karna hoga. Ye command file ko aapke staging area aur working directory dono se remove kar deti hai:
```
$ rm PROJECTS.md
$ git status
```
Agar aap simply file ko rm se delete karte hain, toh ye "Changes not staged for commit" mein dikhai dega. File ki removal ko stage karne ke liye, run karein:
```
$ git rm PROJECTS.md
```
Uske baad, git status aapko confirm karega ki file ki removal stage ho gayi hai aur ye agle commit mein permanently delete ho jayegi.

Agar file modify hui ho ya already staged ho, toh aapko -f option ke sath force removal karna hoga. Kisi file ko apne staging area se remove karte hue usse working directory mein rakhne ke liye, --cached option ka use karein:
```
$ git rm --cached README
```
Aap git rm ke sath file patterns bhi use kar sakte hain, jaise:
```
$ git rm log/*.log
```
Ye command log/ directory mein sabhi .log files ko remove kar dega.

Files Ko Move Karna
Baaki version control systems ke mukable, Git explicitly file movements ko track nahi karta. Lekin, aap file ko rename karne ke liye git mv command ka use kar sakte hain:
```
$ git mv file_from file_to
```
Jaise:
```
$ git mv README.md README
```
Running git status ke baad, Git aapko confirm karega ki file ko rename kiya gaya hai:
```
$ git status
```
### Commit History Dekhna
Apne project ki commit history dekhne ke liye, git log command ka use karein:
```
$ git log
```
Ye command repository mein banaye gaye commits ko reverse chronological order mein list karegi, jismein har commit ka SHA-1 checksum, author, date, aur message dikhai dega:
```
$ git log
commit ca82a6dff817ec66f44342007202690a93763949
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Mon Mar 17 21:52:11 2008 -0700

    Change version number

commit 085bb3bcb608e1e8451d4b2432f8ecbe6306e7e7
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 16:40:33 2008 -0700

    Remove unnecessary test

commit a11bef06a3f659402fe7563abf99ad00de2209e6
Author: Scott Chacon <schacon@gee-mail.com>
Date:   Sat Mar 15 10:31:28 2008 -0700
    Initial commit
```
Default roop se, git log sabse recent commits ko pehle dikhata hai. git log ke liye bohot saare options available hain, jo aapki zarurat ke mutabik output ko customize karte hain.
Basic Command
```
$ git log --pretty=format:"%h - %an, %ar : %s"
```
Output Example:
```
ca82a6d - Scott Chacon, 6 years ago : Change version number
085bb3b - Scott Chacon, 6 years ago : Remove unnecessary test
a11bef0 - Scott Chacon, 6 years ago : Initial commit
```
Useful Specifiers for git log --pretty=format
Specifier	Description of Output
%H	Commit hash
%h	Abbreviated commit hash
%T	Tree hash
%t	Abbreviated tree hash
%P	Parent hashes
%p	Abbreviated parent hashes
%an	Author name
%ae	Author email
%ad	Author date (format respects the --date=option)
%ar	Author date, relative
%cn	Committer name
%ce	Committer email
%cd	Committer date
%cr	Committer date, relative
%s	Subject
###  Author vs. Committer:
Author wo vyakti hota hai jisne kaam likha hai, jabki committer wo hota hai jisne kaam last apply kiya. Agar aap ek patch bhejte hain aur koi core member use apply karta hai, toh dono ko credit milta hai.

Output Formatting Options
--graph: Branch aur merge history ka ASCII graph dikhata hai.
--pretty: Commits ko alternate format mein dikhata hai. Options mein oneline, short, full, aur fuller shamil hain.
-p: Har commit ke saath patch dikhata hai.
Example:
```
$ git log --pretty=format:"%h %s" --graph
```
### Limiting Log Output
Useful Limiting Options:

1. -<n>	Last n commits dikhata hai.
2. --since	Specified date ke baad ke commits dikhata hai.
3. --until	Specified date se pehle ke commits dikhata hai.
4. --author	Specific author ke commits dikhata hai.
5. --grep	Commit messages mein string hone par unhe dikhata hai.
6. -S	Specific string ko add ya remove karne wale commits dikhata hai.
Example Command:
```
$ git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" --before="2008-11-01" --no-merges -- t/
```
- Preventing Merge Commits
Agar aap merge commits ko nahi dikhana chahte, toh --no-merges option add karein.
## Undoing Things in Git
Koi bhi samay, aapko kuch changes ko undo karne ki zarurat ho sakti hai. Yahaan kuch basic tools ka review kiya jayega jo aapne kiye gaye changes ko undo karne ke liye upyog kiye ja sakte hain. Dhyaan rahe, kyunki kuch undos ko aap hamesha undo nahi kar sakte. Ye Git ke kuch aise areas hain jahan galat karne par aap apna kaam kho sakte hain.

Commit Ko Sudharna
Aksar, aap tab commit karte hain jab aapne kuch files ko add karna bhool gaye ho, ya phir aapka commit message galat ho. Agar aap uss commit ko dobara karna chahte hain, to aap bhuli hui changes ko karen, unhe stage karen, aur --amend option ke saath dobara commit karen:
```
$ git commit --amend
```
Ye command aapki staging area ko use karti hai commit ke liye. Agar aapne apne last commit ke baad koi changes nahi kiye hain (jaise ki, aap is command ko apne previous commit ke turant baad chalayate hain), to aapka snapshot waise hi dikhega, aur aap sirf apne commit message ko badlenge.

Commit-message editor khulega, lekin is baar pehle se hi aapke previous commit ka message hoga. Aap message ko edit kar sakte hain jaise aap hamesha karte hain, lekin ye aapke previous commit ko overwrite kar dega.
## Unstaging a Staged File
Agle do sections mein aap dekhenge kaise aap apne staging area aur working directory changes ke saath kaam kar sakte hain. Sabse achi baat ye hai ki jo command aap in areas ke state ko jaanne ke liye use karte hain, wahi aapko unhe undo karne ka tareeka bhi batati hai.

For example, maan lijiye aapne do files mein changes kiye hain aur aap chahte hain ki aap unhe alag-alag commits mein karein. Lekin galti se aap git add * type kar dete hain aur dono ko stage kar dete hain. Ab aap kaise ek file ko unstage karenge? Aapka git status command aapko yaad dilata hai:
```
$ git add *
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
```
"Changes to be committed" ke neeche diya hota hai: "use git reset HEAD <file>... to unstage". To, hum is salah ka use karte hain aur CONTRIBUTING.md file ko unstage karte hain:
```
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M   CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   CONTRIBUTING.md
```
Ye command thoda ajeeb lag sakta hai, lekin kaam karta hai. Ab CONTRIBUTING.md file modified hai lekin unstaged hai.

Note: git reset command dangerous ho sakta hai, khaas kar agar aap --hard flag ka use karte hain. Lekin upar wale example mein, file aapke working directory mein untouched rahti hai, to ye relatively safe hai.

File Ko Unmodify Karna
Agar aap realize karte hain ki aap apni changes ko rakhna nahi chahte jo aapne CONTRIBUTING.md file mein kiye hain, to aap ise easily kaise revert kar sakte hain? Matlab, kaise ise wapas us state mein le ja sakte hain jab aapne ise last commit kiya tha (ya clone kiya tha)? Kismat se, git status aapko iska bhi solution deta hai.

Last example mein, unstaged area kuch aisa dikhta hai:

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   CONTRIBUTING.md
```
Ismein saaf likha hai kaise aap apne changes ko discard kar sakte hain. To chaliye is par amal karte hain:
```
$ git checkout -- CONTRIBUTING.md
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    renamed:    README.md -> README
```
Ab aap dekh sakte hain ki changes revert ho gayi hain.

Lekin ye samajhna zaruri hai ki git checkout -- <file> ek dangerous command hai. Jo bhi local changes aapne is file mein kiye the, wo sab khatam ho jaate hain — Git us file ko last staged ya committed version se replace kar deta hai. Is command ka use tab tak na karein jab tak aap sure na ho ki aap apne local changes ko kho dena chahte hain
## Remotes ke saath kaam karna
Agar aapko kisi bhi Git project mein collaborate karna hai, toh aapko apni remote repositories ko manage karna aana chahiye. Remote repositories aapke project ke aise versions hote hain jo internet ya kisi network par host hote hain. Aapke paas kai remote repositories ho sakte hain, jinmein se kuch read-only ya read/write hote hain. Dusron ke saath collaborate karte waqt, remote repositories ko manage karna aur data ko push aur pull karna zaroori hota hai jab aapko apna kaam share karna hota hai. Remote repositories ko manage karne ke liye aapko unhe add karna, invalid remotes ko remove karna, alag-alag remote branches ko manage karna aur unhe track karna ya nahi karna aana chahiye.

Remote Repositories aapki local machine par bhi ho sakte hain.
Yeh possible hai ke aap ek "remote" repository ke saath kaam kar rahe ho jo asal mein aapki local machine par hi ho. "Remote" ka matlab yeh nahi hota ke repository zaroor kisi aur jagah network ya internet par ho, sirf itna ki yeh kahin aur exist karti hai.

Aap dekh sakte hain ke aapne kaunse remote servers configure kiye hain git remote command se. Agar aapne apna repository clone kiya hai, toh aapko kam se kam origin dikhai dega jo default naam hota hai jise Git server ko assign karta hai jisse aapne clone kiya hai.
```
$ git clone https://github.com/schacon/ticgit
$ git remote
origin
```
Aap -v flag use karke URLs bhi dekh sakte hain jo Git ne fetch aur push ke liye store kiye hain:

```
$ git remote -v
origin  https://github.com/schacon/ticgit (fetch)
origin  https://github.com/schacon/ticgit (push)
```
Remote Repositories ko add karna
Agar aap ek naya remote add karna chahte hain, toh aap git remote add <shortname> <url> command use kar sakte hain:
```
$ git remote add pb https://github.com/paulboone/ticgit
$ git remote -v
origin  https://github.com/schacon/ticgit (fetch)
origin  https://github.com/schacon/ticgit (push)
pb      https://github.com/paulboone/ticgit (fetch)
pb      https://github.com/paulboone/ticgit (push)
```
Apne Remotes se Fetch aur Pull karna
Naya data lane ke liye aap git fetch <remote> use karte hain. Yeh command sirf data ko local repository mein laata hai, automatically merge nahi karta.

Agar aapka branch ek remote branch ko track kar raha hai, toh aap git pull use karke fetch aur merge dono kar sakte hain.

Apne Remotes ko Push karna
Jab aapka project ready ho, toh aap git push <remote> <branch> use karke apna kaam share kar sakte hain. Agar aapke paas write access hai toh aap apne commits ko server par push kar sakte hain:
```
$ git push origin master
```
### Remote ko inspect karna
Agar aap ek remote ke baare mein zyada jaanchna chahte hain, toh git remote show <remote> command use karein.
```
$ git remote show origin
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push URL: https://github.com/schacon/ticgit
  HEAD branch: master
```
Remotes ka naam badalna aur remove karna
Agar aap kisi remote ka naam change karna chahte hain, toh aap git remote rename use kar sakte hain:
```
$ git remote rename pb paul
```
Agar aapko koi remote remove karna hai, toh aap git remote remove use kar sakte hain:
```
$ git remote remove paul
```
## Tag Kya Hai Git Mein?
Tag ek tarike ka label hota hai jo hum Git repository ke kisi specific point ya commit par laga sakte hain. Ye release versions ya koi important milestone ko mark karne ke liye use hota hai, jaise v1.0, v2.0, etc.

#### Git Mein Tag Ke Types
- Lightweight Tag:

Bas ek simple pointer hota hai kisi specific commit par.
Ismein koi extra information, jaise tagger ka naam, email, ya message nahi hota.
Example:
```
$ git tag v1.0
```
- Annotated Tag:

Yeh zyada detailed hota hai. Ismein tagger ka naam, email, date, aur ek message hota hai.
Isko sign bhi kiya ja sakta hai (GPG signature ke sath).
Example:
```
$ git tag -a v1.0 -m "Version 1.0 release"
```
Tag Kaise Create Karein?
Lightweight Tag Banana:
```
$ git tag <tagname>
```
Example:
```
$ git tag v1.0
```
Annotated Tag Banana:

```
$ git tag -a <tagname> -m "Tagging message"
```
Example:
```
$ git tag -a v1.0 -m "Version 1.0 release"
```
Tag List Kaise Dekhein?
Agar tumhe saare tags dekhne hain jo repository mein bane hain, toh yeh command use karo:
```
$ git tag
```
Agar specific pattern ke tags dekhne hain, toh:
```
$ git tag -l "v1.0*"
```
Tag Kaise Delete Karein?
Local Tag Delete Karna:
```
$ git tag -d <tagname>
```
Example:
```
$ git tag -d v1.0
```
Remote Tag Delete Karna:
```
$ git push origin --delete <tagname>
```
Example:

```
$ git push origin --delete v1.0
```
Tag Ko Kaise Push Karein?
Default mein tags push nahi hote jab tum git push karte ho. Isliye manually push karna padta hai.

Single Tag Push Karna:
```
$ git push origin <tagname>
```
Example:
```
$ git push origin v1.0
```
Sare Tags Ek Saath Push Karna:
```
$ git push origin --tags
```
Tag Ko Kaise Checkout Karein?
Agar tumhe kisi specific tag ki state dekhni hai, toh tum tag ko checkout kar sakte ho:

```
$ git checkout <tagname>
```
Example:
```
$ git checkout v1.0
```
Iske baad tum "detached HEAD" state mein chale jaoge, iska matlab tum koi bhi commit karoge toh wo kisi branch se associated nahi hoga. Agar tumhe changes save karne hain toh ek new branch bana sakte ho:
```
$ git checkout -b <branch-name>
```
Tag Ko Kaise Pull Karein?
Agar tum remote repository se tags pull karna chahte ho, toh simply yeh command use karo:
```
$ git fetch --tags
```
## Git Aliases

Git me aliases ka use aap commands ko short form me run karne ke liye kar sakte ho, taki baar baar lambi commands na likhni pade. Aap git config ka use karke apni favorite commands ke aliases bana sakte ho. Yeh kaafi helpful hota hai jab aap frequent commands use karte ho.

Basic Aliases Commands:
Alias Set Karna:
```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```
Example: git checkout ko git co se run karna.
Unstage Command:
```
$ git config --global alias.unstage 'reset HEAD --'
```
Example: git reset HEAD -- fileA ko ab git unstage fileA se run kar sakte ho.
Last Commit Dekhna:
```
$ git config --global alias.last 'log -1 HEAD'
```
Example: git last likhne se aapka latest commit dikh jaayega.
#### Advanced Aliases:
Custom Commands Banana: Agar aap apne custom tools use karte ho jo Git ke saath kaam karte hain, to aap ! ke saath external commands bhi add kar sakte ho.
```
$ git config --global alias.visual '!gitk'
```
Example: git visual likhne par gitk GUI open ho jaayega.
