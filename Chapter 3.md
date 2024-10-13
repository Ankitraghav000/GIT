# Git Branching 

Git branching ka matlab hota hai ki aap apne main project ke line se alag hoke ek nayi line bana sakte ho jisme alag kaam karte ho, bina original code ko touch kiye. Iska fayda yeh hota hai ki aap parallel mein kaam kar sakte ho, changes ko test kar sakte ho, aur jab kaam complete ho jaye to wapas main line mein merge kar sakte ho.

Git mein branches banana aur unke beech switch karna bohot fast aur easy hota hai. Har branch ek alag snapshot jaisi hoti hai jisme aap kaam karte ho, aur jab chahe aap main branch pe waapas aa sakte ho. Branching ka use karke aap apne code ko alag-alag features ya experiments ke liye tod sakte ho, bina core code ko bigade.
## Branches ka Summary
Git ka branching kaise kaam karta hai samajhne ke liye hume pehle yeh dekhna padega ki Git apna data kaise store karta hai.

Jaise ki aapko pehle bataya tha "What is Git?" mein, Git data ko changesets ya differences ke form mein store nahi karta, balki snapshots ke form mein store karta hai.

Jab aap koi commit karte ho, Git ek commit object banata hai jo staged content ke snapshot ka pointer rakhta hai. Is object mein author ka naam, email address, commit ka message, aur us commit ke parent commit ka pointer hota hai: initial commit ke liye koi parent nahi hota, normal commit ke liye ek parent hota hai, aur merge ke case mein do ya zyada parents ho sakte hain.

Isko visualize karne ke liye sochiye aapke paas ek directory hai jisme 3 files hain, aur aap unhe stage karke commit karte ho. Jab aap files ko stage karte ho, Git har ek file ka checksum compute karta hai (jise SHA-1 hash kehte hain) aur un files ko Git repository mein store karta hai. Phir woh checksum ko staging area mein add karta hai
## Creating a New Branch
Jab aap ek nayi branch banate ho, toh Git ek naya pointer banata hai jo aapke current commit ke upar point karta hai. For example, agar aapko ek nayi branch "testing" banani hai, toh aap yeh command use karte ho:
```
$ git branch testing
```
Isse ek naya pointer create hota hai jo usi commit ko point karega jahan aap abhi ho. Samjho ki abhi aap "master" branch pe ho, toh "testing" branch bhi wahi point karegi jahan "master" hai. Ab dono branches ek hi commit ko point kar rahe hain.

## Git HEAD Ka Role
Ab, kaise pata chalega ki aap kis branch pe ho? Iska jawab hai HEAD pointer. Git mein, HEAD ek special pointer hai jo aapki current branch ko point karta hai. For example, abhi aap "master" branch pe ho. Jab aapne git branch command chalayi thi, tab ek nayi branch to ban gayi thi, lekin aap us branch pe switch nahi hue.

Aap ise clearly dekh sakte ho agar aap git log --oneline --decorate command run karte ho:
```
$ git log --oneline --decorate
```
Is command se aap dekh paoge ki kaunsi branch ka pointer kis commit ko point kar raha hai. Kuch output aisa dikhega:
```
f30ab (HEAD -> master, testing) Add feature #32 - ability to add new formats
34ac2 Fix bug #1328 - stack overflow under certain conditions
98ca9 Initial commit
```
Is example mein, aap dekh sakte ho ki "master" aur "testing" dono branches abhi ek hi commit ko point kar rahi hain (commit f30ab).
## Git Mein Branch Switching
Git mein ek existing branch par switch karne ke liye, aap git checkout command ka istemal karte hain. Maan lo, humein testing branch par switch karna hai:
```
$ git checkout testing
```
Is command se HEAD testing branch ko point karega.

Iska Kya Matlab Hai?
Ab agar aap ek commit karte hain:
```
$ vim test.rb
$ git commit -a -m 'Make a change'
```
Is se testing branch aage badh jayegi, lekin aapka master branch ab bhi us commit par point karega jahan aapne checkout command chalai thi.

Master Branch Par Wapas Switch Karna
Ab agar aap master branch par wapas switch karna chahte hain:
```
$ git checkout master
```
Agar aap git log chalate hain, toh aapko shayad yeh samajh nahi aayega ki testing branch kahan gayi, kyunki yeh output mein nahi dikhegi.

Yeh branch gaayab nahi hui hai; Git sirf yeh sochta hai ki aapko kaunsi branch ki history dekhni hai. Default roop se, git log sirf un commits ki history dikhata hai jo aapne checkout ki hui branch ke neeche hain.

Specific Branch Ki History Dikhana
Agar aapko testing branch ki history dekhni hai, toh aapko explicitly specify karna hoga:
```
git log testing
```
Aur agar aap sabhi branches ki history dekhna chahte hain, toh command ko --all option ke saath chalana hoga:
```
git log --all
```
Switching Branches Ke Effects
Jab aap Git mein branches switch karte hain, toh aapke working directory mein files badal jayengi. Agar aap purani branch par switch karte hain, toh aapka working directory us branch par last commit hone par waisa hi ho jayega. Agar Git ise cleanly nahi kar sakta, toh aapko switch karne nahi dega.

Changes Karna Aur Commit Karna
Agar aap kuch changes karte hain aur phir se commit karte hain:

```
$ vim test.rb
$ git commit -a -m 'Make other changes'
```
Ab aapka project history diverge ho chuka hai. Aapne ek branch create ki, uspe kaam kiya, phir master branch par switch karke aur kaam kiya. Dono changes alag branches mein hain, aur aap inhe kabhi bhi merge kar sakte hain jab aap tayaar ho.

Commit History Dekhna
Agar aap git log command chalayenge:
```
$ git log --oneline --decorate --graph --all
```
Yeh command aapke commits ki history dikhayegi, jismein branch pointers aur history ka divergence dikhai dega.

Branch Creation Aur Deletion
Git mein branch actually ek simple file hoti hai jo commit ka 40 character SHA-1 checksum rakhti hai. Branches banana aur hataana bahut aasaan hai, kyunki yeh sirf 41 bytes ka file write karne jaisa hai (40 characters aur ek newline).

Ye Git ke purane VCS tools ke comparison mein bahut fast hai, jahan project ke files ka ek naya copy banta hai.

Nayi Branch Banana Aur Uspar Switch Karna
Agar aap ek nayi branch banana chahte hain aur saath hi uspar switch bhi karna chahte hain, toh aap yeh ek operation mein kar sakte hain:
```
git checkout -b <newbranchname>
```
## Basic Branching aur Merging ka ek simple example

Chalo ek real-world example dekhte hain jisme branching aur merging ka use hota hai. Yeh steps follow karenge:

- Tum apni website pe kuch kaam kar rahe ho.
- Ek naye user story ke liye branch create karo.
- Us branch me kaam karo.
- Is stage pe tumhe ek urgent call milega ki ek aur issue critical hai aur uska hotfix karna padega. Ab yeh steps follow karenge:

- Apni production branch me switch karo.
- Ek branch banao hotfix ke liye.
- Test hone ke baad, hotfix branch ko merge karo aur production pe push karo.
- Phir apni original branch pe wapas aa ke kaam continue karo.
### Basic Branching kaise karein
Maan lo tum already apni project pe kaam kar rahe ho aur master branch pe kuch commits kar diye hain.

Ab tumhe ek naye issue #53 pe kaam karna hai. Uske liye, ek naya branch banate hain aur us branch pe switch karte hain:
```
$ git checkout -b iss53
Switched to a new branch 'iss53'
```
Ab iss naye branch me tum apna kaam karoge, jaise ki footer update karna:
```
$ vim index.html
$ git commit -a -m 'Create new footer [issue 53]'
```
### Urgent Hotfix kaise karein
Tumhe call aaya ki ek urgent hotfix ki zarurat hai. Tumhe apne master branch pe wapas switch karna hoga, taaki tum hotfix kar sako bina iss53 ke changes ko deploy kiye:
```
$ git checkout master
```
Ab tum master branch pe ho, aur hotfix ke liye ek nayi branch banate ho:
```
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
```
Hotfix ke baad, usse master branch me merge karte hain:
```
$ git checkout master
$ git merge hotfix
```
Yeh fast-forward merge ho raha hai, iska matlab koi conflict nahi hai, aur Git simply branch pointer ko aage badha raha hai.

Original Branch pe wapas kaise aayein
Hotfix ka kaam complete hone ke baad, tumhe hotfix branch delete karni hogi, kyunki ab master branch pe wahi changes hain:
```
$ git branch -d hotfix
Deleted branch hotfix.
```
Ab tum apni iss53 branch pe wapas aa ke apna kaam continue kar sakte ho:
```
$ git checkout iss53
```
Basic Merging kaise karein
Agar tumhara issue #53 ka kaam complete ho gaya hai aur tumhe usse master branch me merge karna hai, to yeh steps follow karo:
```
$ git checkout master
$ git merge iss53
```
Agar dono branches ke same file ke same part me changes hue hain, to Git merge conflict show karega. Tumhe conflict resolve karna hoga manually, jaise yeh:

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer"> please contact us at support@github.com </div>
>>>>>>> iss53:index.html
```
Tum dono versions ko merge karke final version banate ho aur phir us file ko stage karte ho:
```
$ git add index.html
```
Merge commit finalize karne ke liye:
```
$ git commit
```
## Branch Management

Ab jab tumne branch create, merge, aur delete karna seekh liya hai, to chalo kuch branch management ke tools dekhte hain jo hamesha branches ka use karte time kaam aayenge.

### Git Branch Command
git branch command sirf branch banata aur delete nahi karta. Agar tum ise bina kisi argument ke run karte ho, to tumhe apne current branches ka ek simple list milta hai:

```
$ git branch
  iss53  
* master  
  testing
```
Yahan * sign master branch ke aage dikh raha hai, jo yeh indicate karta hai ki tum abhi kaunse branch pe ho. Matlab ab agar tum koi commit karte ho, to wo commit master branch pe hoga.

Last Commit Check Karna
Har branch pe last commit dekhne ke liye git branch -v command use kar sakte ho:
```
$ git branch -v
  iss53    93b412c Fix javascript issue
* master   7a98805 Merge branch 'iss53'
  testing  782fd34 Add scott to the author list in the readme
```
### Merged aur Non-Merged Branches
Kuch useful options, jaise --merged aur --no-merged, branch list ko filter karte hain. --merged wo branches dikhata hai jo tumne current branch me merge kar liye hain:
```
$ git branch --merged
  iss53  
* master
```
Yeh list wo branches dikhata hai jo merge ho chuki hain. Tum in branches ko safely delete kar sakte ho, kyunki inka kaam already dusre branch me aa chuka hai:
```
$ git branch -d iss53
```
Agar tum aise branches dekhna chahte ho jinke kaam abhi merge nahi hue hain, to yeh command use karo:
```
$ git branch --no-merged
  testing
```
Ab agar tum testing branch ko delete karne ki koshish karte ho bina usse merge kiye, to yeh error show karega:
```
$ git branch -d testing
error: The branch 'testing' is not fully merged.
```
Agar tum force delete karna chahte ho, to -D option use karna hoga:
```
$ git branch -D testing
```
Doosri Branch pe Merge Status Check Karna
Tum doosri branch ka merge status check karne ke liye argument pass kar sakte ho. Jaise, agar tum yeh dekhna chahte ho ki master branch me kaunse branches abhi tak merge nahi hue hain:
```
$ git branch --no-merged master
  topicA  
  featureB
```
### Branch Name Change Karna
Agar tum ek branch ka naam change karna chahte ho, to yeh steps follow karo. Pehle apni branch ka naam local system pe change karne ke liye yeh command run karo:
```
$ git branch --move bad-branch-name corrected-branch-name
```
Yeh command local branch ka naam badal degi, lekin remote server (jaise GitHub) pe nahi badlegi. Remote pe bhi naam update karne ke liye yeh command run karo:
```
$ git push --set-upstream origin corrected-branch-name
```
Yeh command ke baad tumhare remote pe naya naam reflect hoga. Lekin purana naam ab bhi remote pe hoga. Usse delete karne ke liye yeh command run karo:
```
$ git push origin --delete bad-branch-name
```
Iske baad purana branch naam remove ho jayega aur naya naam use hoga.

Master Branch ka Naam Badalna
Agar tum master branch ka naam badalna chahte ho, to dhyan rakho ki yeh steps sab projects, services, aur scripts ko break kar sakta hai jo master branch pe depend karte hain. Naam change karne se pehle apne team se baat karo.

Local master branch ka naam change karne ke liye:
```
$ git branch --move master main
```
Phir naye branch naam ko remote pe push karo:
```
$ git push --set-upstream origin main
```
Ab tumhare remote pe main branch available hogi, lekin master branch ab bhi wahan hogi. Agar tumhe master branch ko completely hataana hai, to pehle sab configurations aur references ko update karo. Phir master branch ko delete kar do:
```
$ git push origin --delete master
```
## Remote Branches

Remote references pointers hote hain  jo remote repositories mein branches aur tags ko dikhate hain. Aap git ls-remote <remote> ya git remote show <remote> se inka status dekh sakte ho. Remote-tracking branches vo local references hote hain jo remote branches ki state ko track karte hain. Jab aap network communication karte ho, Git inhe update karta hai.

Remote-tracking branches ka format <remote>/<branch> hota hai, jaise origin/master, jo remote master branch ko track karta hai. Jab aap kisi repository ko clone karte ho, Git remote branch ko track karne ke liye aapke local mein origin/master jaise branches create karta hai.
### Local aur Remote Work ka Alag Chalna
Jaise hi aap apne remote ke saath apna kaam sync karna chahte ho, aapko git fetch <remote> command run karni padti hai (humare case mein, git fetch origin). Ye command check karti hai ki "origin" kaun sa server hai (hamare case mein, ye git.ourcompany.com hai), aur koi bhi data fetch karti hai jo ab tak aapke paas nahi hai. Ye aapke local database ko update karti hai aur aapka origin/master pointer ko naye aur updated commit tak le jaati hai.
### Pushing
Git mein agar aapko apni branch remote server par push karni hai, toh aapko kuch commands use karni padengi. Pushing ka matlab hai ki aap apne local repository ke changes ko remote repository mein bhej rahe ho, taaki dusre log bhi unhe dekh aur use kar sakein.

Basic Push Command
Aapko remote repository (jaise origin) aur branch ka naam dena hota hai jise aap push karna chahte ho. Example:
```
$ git push origin master
```
Yeh command aapki local master branch ke changes ko origin remote ke master branch par push kar dega.

Nayi Branch Push Karna
Agar aap ek nayi branch push kar rahe ho, jo remote par ab tak exist nahi karti, toh simply branch ka naam dal kar push kar do:

```
$ git push origin <branch-name>
```
Example:
```
$ git push origin feature-branch
```
Yeh command local feature-branch ko remote par push karegi.

Branch Rename Karke Push Karna
Aap apni local branch ko remote par ek alag naam ke saath push kar sakte ho. Iske liye local branch ke baad remote branch ka naam dena hota hai:
```
$ git push origin <local-branch>:<remote-branch>
```
Example:
```
$ git push origin bugfix:new-feature-branch
```
Yeh command local bugfix branch ko remote par new-feature-branch naam se push karegi.

Password Baar Baar Na Dalna
Agar aap HTTPS URL use kar rahe ho aur baar-baar username aur password dalna nahi chahte, toh aap credential cache set kar sakte ho:
```
$ git config --global credential.helper cache
```
Remote Branch Delete Karna
Agar aap remote par kisi branch ko delete karna chahte ho, toh is command ka use karo:

```
$ git push origin --delete <branch-name>
```
Example:
```
$ git push origin --delete feature-branch
```
Yeh command feature-branch ko remote server se delete kar degi.

Sabhi Remote Changes Ko Update Karna
Push karne se pehle, hamesha git fetch command use karo taaki aapke paas latest remote changes hoon:
```
$ git fetch origin
```
#### Push with Force
Agar push karte waqt conflicts aate hain, aur aapko changes ko zabardasti push karna ho, toh force push karne ke liye:
```
$ git push origin master --force
```
Lekin force push karna risk hota hai, kyunki isse dusre logon ke commits overwrite ho sakte hain.
### Tracking Branch in Git
Tracking branch ek local branch hoti hai jo kisi remote branch ko follow karti hai. Isse git pull aur git push commands remote branch ke saath sync ho jaate hain.

Commands:
Automatically track on clone:
```
$ git clone https://github.com/user/repo.git
```
(Automatically tracks origin/master.)

Create a tracking branch:

```
$ git checkout --track origin/<remote-branch>
```
Example:
```
$ git checkout --track origin/feature-branch
```
Shortcut for tracking branch (auto track):
```
$ git checkout <branch>
```
Set tracking branch manually:
```
$ git branch --set-upstream-to=origin/<remote-branch> <local-branch>
```
Check tracking branches status:
```
$ git branch -vv
```
### Pulling in Git
Pulling ka matlab hota hai ki aap apne local repository ko remote repository ke latest changes ke saath sync karte hain. git pull command do kaam karta hai: pehle changes fetch karta hai aur phir unhe merge karta hai.

Common git pull Commands:
- Basic git pull: Remote branch se latest changes fetch aur merge karta hai.
```
$ git pull
```
(Ye command current branch ke remote-tracking branch ko pull karta hai.)

Specific branch ko pull karna: Agar aap ek specific branch ko pull karna chahte ho:
```
$ git pull origin <branch-name>
```
Example:
```
$ git pull origin master
```
Fetch aur merge ko manually karna: Pull ke bajaye aap fetch aur merge alag alag bhi kar sakte ho:

Fetch latest changes:
```
$ git fetch origin
```
Merge changes manually:
```
$ git merge origin/<branch-name>
```
Rebase ke saath pull karna: Agar aap pull karte waqt merge ki jagah rebase karna chahein:
```
$ git pull --rebase
```
All branches ke liye pull: Sabhi branches ke changes ko pull karne ke liye pehle fetch karein, fir manually merge karein:

```
$ git fetch --all
$ git merge
```
Pull without merge conflicts automatically: Agar aap auto-merge karna chahte ho bina manual conflicts handle kiye:
```
$ git pull --no-commit
```
### Rebase
Rebasing ka matlab hai ek branch ke commits ko doosri branch ke latest snapshot ke upar apply karna. Jab aap rebase karte ho, Git aapke commits ko ek ek karke nayi base branch ke upar apply karta hai. Isse ek linear history ban jaati hai, jo clean aur simple dikhayi deti hai.

Rebase ko detail mein samajhne ke liye, hum isse step by step breakdown karte hain.

- Step 1: Current Situation Ko Samjho
Aapke paas do branches hain:

Master branch (main branch jisme final code hota hai)
Experiment branch (jisme aapne kuch naye features add kiye hain)
Donon branches mein commits alag alag hue hain:

master: C1 → C2 → C3
experiment: C4 (experiment branch master se alag ho gayi)
Ab aap chahte ho ki experiment branch ke commits ko master branch ke latest commits ke upar shift karo.

Step 2: Experiment Branch Pe Switch Karna
Sabse pehle, aapko experiment branch pe checkout karna hoga taaki aap usi branch ko rebase kar sakein.

Command:
```
$ git checkout experiment
```
Is command se aap experiment branch pe switch ho jaoge.

Step 3: Master Branch Ke Upar Rebase Karna
Ab, aap experiment branch ko master branch ke upar rebase karenge. Iska matlab hai ki jo changes aapne experiment branch mein kiye hain, wo master ke latest commits ke upar se reapply kar diye jaayenge.

Command:
```
$ git rebase master
```
Ye command kuch steps follow karta hai:

Donon branches ka common ancestor commit dhundta hai (jo C2 hoga).
experiment ke commits (C4) ko temporarily store karta hai.
experiment branch ko master ke latest commit (C3) pe le aata hai.
C4 ke changes ko C3 ke upar se reapply karta hai.
Output kuch aisa dikh sakta hai:

```
First, rewinding head to replay your work on top of it...
Applying: added feature in experiment
```
Ab history kuch aisi ho jaayegi:

master: C1 → C2 → C3
experiment: C1 → C2 → C3 → C4' (C4 ko ab C3 ke upar apply kiya gaya hai)
Step 4: Conflict Resolve Karna (Agar Ho Toh)
Kabhi kabhi, rebase karte waqt conflicts ho sakte hain. Agar aisa hota hai, toh Git aapko conflicts dikhayega aur aapko unhe manually resolve karna padega.

File conflicts ko manually theek karo.

Resolve karne ke baad, staging area mein dalne ke liye command use karo:
```
$ git add <conflicted-file>
```
Phir rebase ko continue karne ke liye:
```
$ git rebase --continue
```
Step 5: Fast-forward Merge Karna (Optional)
Ab agar aap master branch pe switch karte ho aur changes ko merge karte ho, toh wo ek fast-forward merge hoga. Fast-forward merge ka matlab hai ki master ka pointer experiment ke latest commit pe move kar jayega bina koi naya merge commit create kiye.

Commands:
```
$ git checkout master
$ git merge experiment
```
Iske baad master branch pe history kuch aisi dikhayi degi:

master: C1 → C2 → C3 → C4'
History ab clean aur linear hai, koi extra merge commit nahi hai.

Step 6: Rebase Ko Cancel Karna (Agar Kuch Galat Ho Jaaye)
Agar rebase ke dauran kuch galat ho jaata hai aur aap purane state mein wapas jaana chahte ho, toh aap rebase ko abort kar sakte ho.

Command:
```
$ git rebase --abort
```
Is command se aapka rebase process cancel ho jayega aur sab kuch wapas purane state mein aa jayega.

