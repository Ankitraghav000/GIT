# Distributed Git
Ab jab aapne remote Git repository setup kar liya hai jise sabhi developers apne code share karne ke liye istemal karte hain, aur aap local workflow mein basic Git commands ke saath parichit hain, aap dekhenge ki Git ke distributed workflows kaise kaam karte hain.

Is chapter mein, aap Git ko distributed environment mein ek contributor aur integrator ke roop mein kaise istemal karein, yeh seekhenge. Aap seekhenge ki ek project mein code kaise successfully contribute karein aur project maintainer ke liye ise asan bana dein, aur kaise ek project ko kai developers ke saath milkar successfully maintain karein.

## Distributed Workflow in Git
Git ke distributed workflow se developers ko projects par kaam karne ki zyada flexibility milti hai. Isme har developer apne local repository ka istemal karke code bana sakta hai aur dusre developers ke saath asaani se share kar sakta hai. Yahan kuch common distributed workflows hain:

### Centralized Workflow
Centralized systems mein, ek hi collaboration model hota hai — centralized workflow. Ek central hub ya repository code accept karta hai, aur sab log apne kaam ko uske sath synchronize karte hain.

Workflow:

Multiple developers hub se clone karte hain.
Pehla developer apne changes push karta hai.
Dusra developer apne changes push karne ki koshish karta hai, lekin server unhe reject kar deta hai. Unhe pehle changes fetch aur merge karne hote hain.
Is workflow ko bahut log pasand karte hain kyunki yeh unke liye familiar aur comfortable hai.
#### Dictator aur Lieutenants Workflow

Yeh ek variant hai multiple-repository workflow ka, jo bade projects mein use hota hai jisme kai saare collaborators hote hain, jaise Linux kernel. Isme kai integration managers hote hain jo repository ke alag-alag parts handle karte hain, inhe lieutenants bola jata hai. Inke upar ek integration manager hota hai, jo benevolent dictator kehlaata hai. Dictator apne directory se ek reference repository tak push karta hai, jahan se saare collaborators ko apna kaam pull karna hota hai.

Process kuch is tarah hota hai:

Regular developers apne topic branch par kaam karte hain aur apna kaam master branch par rebase karte hain. Master branch wo hoti hai jo dictator reference repository mein push karta hai.
Lieutenants developers ke topic branches ko apne master branch mein merge karte hain.
Dictator lieutenants ke master branches ko apne master branch mein merge karta hai.
Aakhir mein, dictator apne master branch ko reference repository tak push karta hai, taki baaki developers uspe apna kaam rebase kar sakein.
Yeh workflow zyada common nahi hai, lekin bade projects ya hierarchical environments mein useful ho sakti hai. Isse project leader (dictator) ko kaafi kaam delegate karne ka mauka milta hai aur kai points par code ko collect karne ka chance milta hai final integration se pehle.

### Contributing to a Project

Git kaafi flexible hai, aur har project ka apna contribution process hota hai. Contribution ka tareeka depend karta hai kuch factors par, jaise:

Active Contributor Count: Kitne log actively contribute kar rahe hain? Bade projects mein zyada contributors aur commits hote hain, isliye aapka code up to date rakhna zaroori hota hai.

Workflow: Project centralized hai ya koi maintainer sab patches check karta hai? Kya patches peer-reviewed hote hain? Kya lieutenant system follow hota hai?

Commit Access: Agar aapke paas write access nahi hai, to project kaise contributions accept karta hai? Kitna aur kitni baar contribute karna hota hai?

Yeh sab factors decide karte hain ki aap kaise effectively contribute karenge.

### Commit Guidelines
Commit messages aur commits kaise banayein yeh samajhna important hai jab aap Git mein kaam kar rahe hain. Yaha kuch zaroori points hain jo aapko follow karne chahiye:

-Whitespace Errors Avoid Karo:
Git mein commit karne se pehle git diff --check chalakar whitespace errors check kar lo. Isse aap avoid kar sakte ho ki baaki developers ko dikkat ho.

- Separate Changesets Banao:
  Har commit ek logical aur alag change hona chahiye. Ek hi commit mein sab kuch daalne ki jagah, har issue ke liye alag commit karo. Agar ek hi file mein multiple changes hain, to git add --patch use karke unhe split kar sakte ho.

- Quality Commit Messages Likho:
 Commit message short aur clear hona chahiye (50 characters se kam), aur imperative tone mein likho jaise "Fix bug", "Add feature".
## Private Small Team Workflow 

Yeh workflow tab kaam aata hai jab ek private project mein 2-3 developers kaam karte hain. "Private" ka matlab hai ki yeh closed-source project hai, jo publically accessible nahi hai. Sabhi developers ko repository par push karne ka access hota hai.

#### Workflow Ka Overview:

##### Clone Repository: 
Dono developers apne systems par repository ko clone karte hain.

John: $ git clone john@githost:simplegit.git
Jessica: $ git clone jessica@githost:simplegit.git
##### Commit Changes:
Dono apni machines par kaam karte hain aur local commits banate hain.

John: git commit -am 'Remove invalid default value'
Jessica: git commit -am 'Add reset task'
Push Changes: Jessica apne changes ko server par push karti hain:
```
$ git push origin master
```
##### Push Conflict: 
Jab John apne changes push karne ki koshish karta hai, to error aati hai kyunki Jessica ne pehle push kiya hota hai:

error: failed to push some refs to 'john@githost:simplegit.git'

###### Fetch and Merge: 
John ko pehle Jessica ke changes fetch karke apne local repository mein merge karna padega:
```
Fetch: $ git fetch origin
Merge: $ git merge origin/master
```
##### Push Again: 
Merge ke baad, John apne merged code ko server par push kar deta hai:
```
$ git push origin master
```
##### Branching Example: 
Jessica ek naya branch issue54 banati hai aur usme commit karti hai. Jab usko pata chalta hai ki John ne naye changes push kiye hain, to wo fetch karti hai:
```
$ git fetch origin
```
Log Check: Jessica check karti hai ki John ke changes se usko kya merge karna hoga:
```
$ git log --no-merges issue54..origin/master
```
##### Merge and Push:
Jessica apna topic branch aur John ke changes merge karti hai, aur phir sab kuch server par push kar deti hai:
```
$ git merge issue54 $ git merge origin/master $ git push origin master
```
## Private Managed Team
Is workflow mein, developers pehle apne branches par kaam karte hain, phir jab ready hota hai, changes ko master branch mein merge karke server par push karte hain.
Yeh scenario ek bade private group ke contributor roles ka hai, jahan pe chhoti teams ek feature pe kaam karti hain, aur unka kaam baad mein doosri team ke members ya integrators ke dwara main repo mein merge hota hai.

Jessica ka workflow: Jessica ke paas repository already cloned hai, toh pehle woh featureA pe kaam shuru karti hai. Uske liye woh ek nayi branch banati hai aur usme kaam karti hai:

##### Jessica's Machine
```
$ git checkout -b featureA
Switched to a new branch 'featureA'
$ vim lib/simplegit.rb
$ git commit -am 'Add limit to log function'
[featureA 3300904] Add limit to log function
```

Ab Jessica ko John ke saath apna kaam share karna hai. Kyunki Jessica ke paas master branch pe push karne ka access nahi hai, woh apne featureA branch ko server pe push karti hai:

```
$ git push -u origin featureA
```
Jessica email bhejti hai John ko batane ke liye ki usne apna kaam featureA branch pe push kar diya hai. Jab tak John ka feedback aata hai, Jessica featureB pe Josie ke saath kaam shuru karti hai. Iske liye woh ek nayi branch server ke master branch se banati hai:

##### Jessica's Machine
```
$ git fetch origin
$ git checkout -b featureB origin/master
Switched to a new branch 'featureB'
```
FeatureB branch pe kuch commits karti hai:
```
$ vim lib/simplegit.rb
$ git commit -am 'Make ls-tree function recursive'

$ vim lib/simplegit.rb
$ git commit -am 'Add ls-files'
```
Jessica ko Josie ka email aata hai ki featureBee branch already server pe hai, toh Jessica pehle Josie ke changes ko merge karti hai:

```
$ git fetch origin
$ git merge origin/featureBee
```
Phir Jessica apna kaam push karti hai featureBee branch pe:

```
$ git push -u origin featureB:featureBee
```
Jessica ko John ka message milta hai ki usne featureA pe kuch changes kiye hain. Jessica woh changes fetch karti hai:
```
$ git fetch origin
```
Phir woh John ke changes ko merge karti hai aur apna final kaam server pe push karti hai:

```
$ git merge origin/featureA
$ git commit -am 'Add small tweak to merged content'
$ git push
```
Last mein, Jessica, Josie, aur John integrators ko batate hain ki featureA aur featureBee branches integration ke liye ready hain.
#### Forked Public Project

Forked Public Project me contribute karna thoda alag hota hai, kyunki aapko directly project ke branches ko update karne ka permission nahi hota. Isliye aapko apne kaam ko maintainers tak kisi aur tareeke se pahuchana padta hai. Ye example forking ke through contribute karna samjhata hai, jo kaafi hosting sites pe support hota hai, jaise GitHub, BitBucket, repo.or.cz, etc. Zyada tar maintainers isi style me contribution expect karte hain. Agle section me hum email ke zariye patches submit karne waale projects ke baare me jaanenge.

Sabse pehle, aapko shayad main repository ko clone karna pade, ek topic branch banana pade for the patch ya patch series jise aap contribute karna chahte hain, aur fir waha kaam karna hoga. Iska sequence kuch is tarah dikhega:

```
$ git clone <url>  
$ cd project  
$ git checkout -b featureA
... kaam karein ...  
$ git commit
... kaam karein ...  
$ git commit
```
Aap rebase -i ka use kar sakte hain apne kaam ko ek single commit me squash karne ke liye, ya phir commits ko arrange kar sakte hain taaki patch maintainers ke liye review karna easy ho. Zyada information ke liye Rewriting History dekh sakte hain.

Jab aapka branch work complete ho jaye aur aap maintainers ko contribute karne ke liye ready ho, to project page pe jaake “Fork” button click karein, jisse aapka writable fork ban jata hai project ka. Phir aapko us repository ka URL apne local repository me ek nayi remote ke roop me add karna hoga; is example me hum ise myfork bolte hain:
```
$ git remote add myfork <url>
```
Aapko apna kaam is repository me push karna hoga. Sabse asaan hai apne topic branch ko forked repository me push karna, instead of apne kaam ko master branch me merge karke push karna. Iska reason ye hai ki agar aapka kaam accept nahi hota ya cherry-pick hota hai, to aapko apne master branch ko rewind nahi karna padega. Agar maintainers merge, rebase, ya cherry-pick karte hain, to aapko eventually apna kaam unki repository se pull karke waapas mil jayega.

Kisi bhi haal me, aap apna kaam is tarah push kar sakte hain:
```
$ git push -u myfork featureA
```
Jab aapka kaam aapke forked repository pe push ho jaye, to aapko original project ke maintainers ko notify karna hoga ki aapke paas kuch kaam hai jo aap chaahte hain ki wo merge karein. Isay aksar pull request kehte hain, aur aap aise request ya to website ke through generate kar sakte hain — GitHub ka apna “Pull Request” mechanism hai jiske baare me hum GitHub section me padhenge — ya aap git request-pull command run karke manually project maintainer ko email kar sakte hain.

git request-pull command base branch leta hai jisme aap apne topic branch ko pull karwana chahte hain aur Git repository URL jisme se aap chahte hain ki wo pull karein. Ye command ek summary generate karta hai saari changes ki jo aap chahte hain pull ho. Example ke liye, agar Jessica ko John ko pull request bhejna hai, aur usne apne topic branch pe do commits kare hain, to wo ye run kar sakti hai:
```
$ git request-pull origin/master myfork
```
Is output ko maintainer ko bheja ja sakta hai — ye batata hai ki kaam kahan se branched tha, commits ka summary deta hai, aur ye bhi batata hai ki naya kaam kahan se pull kiya jana chahiye.

Aap jaha project ke maintainer nahi hain, waha ye easy hota hai ki aapki master branch hamesha origin/master ko track kare aur aap apna kaam topic branches me karein jo aap aasani se discard kar sakein agar wo reject ho jayein. Topic branches me kaam rakhna aapke liye aasaan banata hai apne kaam ko rebase karna agar main repository ka tip badal gaya ho aur aapke commits cleanly apply nahi ho rahe ho. Example ke liye, agar aap project ko dusra topic ka kaam submit karna chahte hain, to aap topic branch pe kaam continue mat karein jo aapne abhi push kiya hai — main repository ke master branch se dubara shuru karein:

```
$ git checkout -b featureB origin/master  
... kaam karein ...  
$ git commit  
$ git push myfork featureB  
$ git request-pull origin/master myfork  
... email generated request pull to maintainer ...  
$ git fetch origin
```
Is tarah se aapke topics alag-alag contained hote hain — ek patch queue ki tarah — jo aap easily rewrite, rebase, aur modify kar sakte hain bina kisi topic ke interfere ya interdependent hone ke, is tarah se:
```
$ git checkout featureA  
$ git rebase origin/master  
$ git push -f myfork featureA
```
Aur yadi maintainers aapke kaam ko like karte hain, par kuch implementation detail change karna chahte hain, to aap apna kaam naya branch bana ke, conflicts resolve karke, aur push karke resubmit kar sakte hain:

```
$ git checkout -b featureBv2 origin/master  
$ git merge --squash featureB  
... change implementation ...  
$ git commit  
$ git push myfork featureBv2
```
Is point pe, aap maintainers ko notify kar sakte hain ki aapne requested changes kar liye hain, aur wo unhe aapke featureBv2 branch me pa sakte hain.
### Maintaining a Project:
Aapko project contribute karne ke saath, usko maintain karna bhi seekhna padega. Jaise ki patches accept karna jo aapko email se mile ya remote branches se changes merge karna. Agar aap project ka main repository maintain kar rahe ho ya patches verify/approve kar rahe ho, toh yeh process aapke liye aur contributors ke liye easy hona chahiye.

Topic Branches mein Kaam karna: Naye kaam ko integrate karne se pehle, ek topic branch banake try karna better hota hai. Jaise agar aap koi ruby_client ka kaam try kar rahe ho, toh aap aise branch bana sakte ho:
```
$ git checkout -b sc/ruby_client master
```
Is tarah se aap naye kaam ko test karke dekh sakte ho bina main branch ko effect kiye.

Email se Patches Apply karna: Agar aapko email se patch mila hai, toh aap git apply ya git am command ka use kar ke usse apply kar sakte ho.

git apply: Agar patch git diff se bana hai, toh aap ise aise apply karenge:
```
$ git apply /tmp/patch-ruby-client.patch
```
Yeh files ko modify karega, lekin commit nahi karega. Aapko manually stage karke commit karna padega.

git am: Agar patch git format-patch se bana hai, toh git am se aap commit info ke saath patch apply kar sakte ho:
```
$ git am 0001-limit-log-function.patch
```
Yeh patch ko commit message aur author info ke saath apply kar deta hai. Agar conflicts aaye, toh aap git am --resolved ya git am --abort ka use kar sakte ho.

Is tarah aap patches ko apply karke unhe aage merge kar sakte ho.
### Cherry-Pick in Git 
Cherry-pick ka use tab hota hai jab aap kisi ek specific commit ko ek branch se utha kar dusri branch me daalna chahte ho bina puri branch ko merge kiye. Iska matlab hai ki aap ek particular kaam ya change ko extract kar ke dusri branch me le jaa sakte ho.

Step-by-Step Cherry-Pick Process:
Branch Select karo: Sabse pehle aapko us branch pe jaana hoga jisme aap commit ko cherry-pick karna chahte ho.
```
git checkout master
```
Yahaan master woh branch hai jisme aap commit lana chahte ho.

Commit ID Pata Karo: Jis commit ko cherry-pick karna hai uska commit ID find karo. Aap git log command ka use karke yeh dekh sakte ho.

```
git log
```
Cherry-Pick Command: Jab aapko commit ID mil jaaye (maan lo e43a6 commit ID hai), tab cherry-pick command run karo:
```
git cherry-pick e43a6
```
Isse woh specific commit aapki current branch me aajayega, lekin ek naya commit ID generate hoga kyunki yeh commit ek naye time pe apply kiya jaa raha hai.

Conflict Resolution (Agar Hoti Hai): Agar koi conflict aata hai to aapko conflicts resolve karna padega. Once resolved, changes ko stage karke commit kar do.

Cherry-Pick Done: Ab cherry-picked commit aapki current branch me successfully add ho gaya hai.

### Rerere in Git
Rerere ka full form hai "Reuse Recorded Resolution". Jab aap baar-baar same conflicts face karte ho, yeh feature un conflicts ko record karke rakhta hai. Agle time jab waise hi conflicts aate hain to Git unhe automatically resolve kar deta hai, bina aapko manually karna pade.

Step-by-Step Rerere Process:
Rerere Enable Karo: Sabse pehle rerere feature ko enable karna hota hai taaki Git conflicts ko yaad rakh sake. Aap yeh global config me set kar sakte ho:
```
git config --global rerere.enabled true
```
Conflicts Resolve Karo: Jab bhi aap merge ya rebase karte ho aur koi conflict aata hai, to aap manually conflict resolve karte ho. Rerere is conflict resolution ko yaad rakhta hai.

Pehle aapko conflict ko dekhna hoga:
```
git status
```
Phir conflicts ko manually fix karo, files ko stage karo:
```
git add <conflicted-file>
```
Resolution Record Ho Gaya: Jab aap conflict ko resolve karte ho aur stage karte ho, rerere us resolution ko record kar leta hai. Next time jab same conflict aayega, Git use automatically fix kar dega.

Next Merge/Rebase: Jab aap agli baar merge ya rebase karoge aur waisa hi conflict aayega, rerere us resolution ko dubara use karega bina aapse manually resolve karaye.

Rerere Commands : Aap rerere ke kuch extra commands ka use karke specific conflicts ko dekh ya clear kar sakte ho:

Dekho kaunse conflicts record hue hain:
```
git rerere status
```
Agar koi specific conflict ko cache se hataana hai:
```
git rerere forget <file>
```



