# Git Tools 
Ab tak aapne Git ke daily use hone waale commands aur workflows seekh liye hain, jaise files ko track karna, commit karna, staging area ka use, aur branching aur merging. Ab aap Git ke kuch powerful features explore karenge jo roz nahi, lekin kabhi kabhi kaam aa sakte hain.
# Revision Selection
Git mein aap ek single commit, commits ka set, ya range ko kaafi tareekon se refer kar sakte ho. Aap kisi commit ko uske 40-character SHA-1 hash se refer kar sakte ho, lekin human-friendly tareeke bhi hain. Agar aap SHA-1 hash ke pehle kuch characters (kam se kam 4) dete ho, to Git samajh jaata hai ki kaunsa commit hai, jab tak wo unique ho.
```
$ git show 1c002dd4b536e7479fe34593e72e6c6c1819e53b
$ git show 1c002dd4b536e7479f
$ git show 1c002d
```
Git aapke SHA-1 hash ke liye ek short, unique abbreviation samajh sakta hai. Agar aap --abbrev-commit option use karte ho git log ke saath, to output mein shorter values dikhai deti hain, jo default mein 7 characters ki hoti hain. Zarurat padne par yeh lamba ho jaata hai taaki SHA-1 unique rahe. Example:
```
$ git log --abbrev-commit (branch name)
```
# Branch References
Agar kisi commit branch ke tip par hai, to aap branch name use karke usse refer kar sakte ho. Jaise:
```
$ git show branch1
```
Agar aapko dekhna hai ki branch kaunsa SHA-1 point kar raha hai, to git rev-parse command use kar sakte ho. Example:
```
ankit@ankit:~/MUSIC-PAGE$ git rev-parse branch1
929d46f05a57cecf57f694ded8387fa075ffdc7f
```
# RefLog Shortnames
Git jab aap kaam kar rahe hote hain, tab background mein ek 'reflog' rakhta hai—yeh log hai jo aapke HEAD aur branch references ke pichle kuch mahine ke location ko track karta hai.
Aap apna reflog dekhne ke liye git reflog command use kar sakte ho:
```
$ git reflog
```
Yeh jaan lena zaruri hai ki reflog information strictly local hoti hai—yeh sirf us cheez ka log hai jo aapne apne repository mein kiya hai. Dusre kisi ke repository copy par references same nahi honge; aur jab aap pehli baar kisi repository ko clone karte hain, to aapka reflog khali hoga, kyunki aapke repository mein abhi tak koi activity nahi hui hoti.
Agar aap reflog information ko git log ke output ki tarah format mein dekhna chahte hain, to aap git log -g run kar sakte ho
```
$ git log -g (branch name)
```
Agar aap git show HEAD@{2.months.ago} run karte hain, to yeh matching commit tabhi dikhayega jab aapne project ko kam se kam do mahine pehle clone kiya ho—agar aapne ise isse recent mein clone kiya, to aapko sirf aapka pehla local commit dikhai dega.
# Ancestry References
Git mein aap commit ko uski ancestry se refer kar sakte ho. Agar aap reference ke end mein ^ (caret) lagate ho, to Git us commit ka parent dikhata hai. Example:
```
$ git show (branch name)^
```
Yeh command aapke Git repository ka commit history ek graphical format mein dikhati hai. Yahaan:
```
git log --pretty=format:'%h %s' --graph
```
- %h se commit ka short hash dikhaya jata hai.
- %s se commit message show hoti hai.
-  --graph option ek graphical representation banata hai jo branch aur merge structure ko easily samajhne mein madad karta hai.

Isse aapko ek clean aur concise history view milta hai jo branches aur merges ko samajhne mein help karta hai.

Yeh command current commit ka parent dikhata hai. Merge commits ke case mein, aap ^2 likhkar second parent bhi dekh sakte ho:
```
$ git show (branch name)^2
```
Tilde ~ bhi parent ko refer karta hai, lekin yeh ek step pehle ke parent tak jata hai. Jaise, (branch name)~2 ka matlab hai "pehle parent ka parent":
```
$ git show (branch name)~2
```
# Commit Ranges
agar aapke paas bahut saari branches hain, toh aap range specifications ka istemal karke yeh jaan sakte hain ki “Is branch mein kya kaam hai jo maine abhi tak apni main branch mein merge nahi kiya hai?

Agar aap dekhna chahte hain ki aapki experiment branch mein kya hai jo abhi tak aapki master branch mein merge nahi hua, toh aap Git se keh sakte hain:
```
$ git log master..experiment
```
Agar aap doosri taraf dekhna chahte hain — saare commits master mein jo experiment mein nahi hain — toh aap branch names ko reverse kar sakte hain.
```
$ git log experiment..master
```
Ek aur aam istemal is syntax ka yeh hai ki aap dekh sakte hain ki aap kya remote par push karne wale hain:
```
$ git log origin/master..HEAD
```
```
$ git log origin/master..
```
Yahaan Git ek taraf missing hone par HEAD ko substitute kar deta hai.
## Multiple Points
Agar aapko do se zyada branches ko specify karna hai, toh Git ^ character ya --not ka istemal karke yeh karne ki suvidha deta hai. 
Agar aap yeh dekhna chahte hain ki refA ya refB mein kaunse commits hain jo refC se reachable nahi hain, toh:
```
$ git log refA refB ^refC
$ git log refA refB --not refC
```
## Triple Dot
Triple-dot syntax un commits ko specify karta hai jo do references mein se kisi ek se reachable hain lekin dono se nahi. Example ke liye:
```
$ git log master...experiment
```
Isse sirf un commits ka information milega jo dono branches ke common references nahi hain.
# Interactive Staging
Interactive Staging ke andar hum alag-alag braches ke through jo changes hue hai unhe ek bar me he stage kar sakte hai.
```
$ git add -i  
          staged     unstaged path  
 1:    unchanged        +0/-1 TODO  
 2:    unchanged        +1/-1 index.html  
 3:    unchanged        +5/-1 lib/simplegit.rb  
*** Commands ***  
 1: [s]tatus  
 2: [u]pdate  
 3: [r]evert  
 4: [a]dd untracked  
 5: [p]atch  
 6: [d]iff  
 7: [q]uit  
 8: [h]elp  
What now>
```
Yeh command aapko staged aur unstaged changes ka ek concise view dikhata hai, jo aap git status mein dekhte hain, par yeh aur zyada informative hota hai. Yeh aapko left mein staged aur right mein unstaged changes dikhata hai

- Agar aap u ya 2 (update ke liye) type karte hain, to aap se poocha jayega ki aap kaunsi files ko stage karna chahte hain:
-sterisk (*) file ke next aata hai jo select ki gayi hai staging ke liye. Agar aap Enter press karte hain bina kuch type kiye, Git selected files ko stage kar dega:

  Isi trarah aap ek ek karke sabhi options ko explore kar sakte hai.
# Staging Patches

Git mein aap files ke kuch parts ko stage kar sakte ho, baaki ko nahi. Jaise agar aapne apne simplegit.rb file mein do changes kiye hain aur aap sirf ek change ko stage karna chahte ho, toh Git mein yeh kaafi aasaan hai. Pehle batayi gayi interactive prompt se, aap "p" ya "5" (patch) type karo. Git aapse poochega ki kaunsi file ka hissa aapko stage karna hai; fir har section ke liye, woh file ka diff hunk dikhayega aur poochega ki kya aap usse stage karna chahte ho:
```
diff --git a/lib/simplegit.rb b/lib/simplegit.rb  
index dd5ecc4..57399e0 100644  
--- a/lib/simplegit.rb  
+++ b/lib/simplegit.rb  
@@ -22,7 +22,7 @@ class SimpleGit  
   end
  
   def log(treeish = 'master')  
-    command("git log -n 25 #{treeish}")  
+    command("git log -n 30 #{treeish}")  
   end
  
   def blame(path)  
```
Stage this hunk [y,n,a,d,/,j,J,g,e,?]?
Aapke paas kaafi saare options hain. Agar aap ? type karoge toh aapko options ki list dikhayi degi:
```Stage this hunk [y,n,a,d,/,j,J,g,e,?]? ?  
y - is hunk ko stage karo  
n - is hunk ko stage mat karo  
a - is hunk aur baaki sab hunks ko stage karo  
d - is hunk ko aur baaki sab hunks ko stage mat karo  
g - ek hunk chunne ke liye  
/ - ek regex match karne wale hunk ko search karo  
j - is hunk ko undecided chhodo, agla undecided hunk dekho  
J - is hunk ko undecided chhodo, agla hunk dekho  
k - is hunk ko undecided chhodo, previous undecided hunk dekho  
K - is hunk ko undecided chhodo, previous hunk dekho  
s - current hunk ko chhote hunks mein split karo  
e - manually current hunk edit karo  
? - help dikhaye
```
<b> Note </b>
- Aapko interactive mode mein hone ki zarurat nahi hai partial-file staging ke liye — aap command line par git add -p ya git add --patch use karke bhi ye kar sakte ho.
Iske alawa, aap patch mode ko files ko partially reset karne ke liye git reset --patch use kar sakte hai.

# Stashing and Cleaning in Git
Kabhi-kabhi jab aap apne project par kaam kar rahe hote ho, toh cheezein thodi messy ho sakti hain, aur aapko kuch aur kaam karne ke liye branch switch karna hota hai. Problem yeh hoti hai ki aap apna half-done work commit nahi karna chahte, taki baad mein uss point par waapas aa sakein. Is problem ka solution hai git stash command. git stash command command ka use karke hum apni file ko secure kar sakte hai.

Agar aap branch switch karna chahte ho bina changes ko commit kiye, toh aap changes ko stash kar sakte ho git stash ya git stash push command ke saath.
```
$ git stash  or $ git stash push
```
agar aap kisi dusri branch par changes apply krna chate hai to ye command use kar sakte hai.
```
$ git stash apply
```
Agar aap specific stash apply karna chahte hain, toh stash name ke saath apply kar sakte hain:
```
git stash list
$ git stash drop stash@{0}
```
New branch banakar stash apply karna:
```
git stash branch (new branch)
```
Agar aapko apne working directory se kuch files ko hata dena hai bina stash kiye, toh git clean command use hota hai. Yeh command untracked files ko remove karta hai. Agar aap dekhna chahte hain ki kaunse files remove honge, toh -n ya --dry-run option ke saath run karein:
```
$ git clean -n -d
```
# Signing Your Work
Git cryptographically secure hai, lekin yeh foolproof nahi hai. Agar aap internet se dusron ka kaam le rahe hain aur yeh verify karna chahte hain ki commits waqai mein trusted source se hain, toh Git ke paas kuch tareeke hain jisse aap apna kaam sign aur verify kar sakte hain GPG ke zariye.
#gpg key setup aap google ya chatgpt ki help se karsakte hai.
Ek baar jab aapke paas private key hai, aap Git ko ise sign karne ke liye configure kar sakte hain:
```
$ git config --global user.signingkey (private key)
```
Agar aapke paas GPG private key set up hai, toh aap naye tags ko sign kar sakte hain. 
```
$ git tag -s v1.5 -m 'my signed 1.5 tag'
```
### Tags Ki Verification
  Yeh command GPG ka istemal karke signature verify karti hai. 
  ```
$ git tag -v v1.5
```
# Searching
Aapko aksar koi function kaha par call ya define kiya gaya hai.Git kuch useful tools provide karta hai jo code aur commits ko jaldi aur aasani se search karne mein madad karte hain.
```
$ git grep -n (FILE NAME )
```
Agar aapko matches ki jagah file count chahiye, toh -c ya --count option ka use karein:
```
$ git grep --count (TEXT/FILE NAME)
```
### Git Log Searching
Agar aapko ye jaanne ki zarurat ho ki koi term kab exist hui ya introduce hui thi, toh git log ka use karke specific commits ko search karna mumkin hai.
```
$ git log -S (commit name) --oneline
```
# Rewriting History
aap already hui commits ko rewrite kar sakte hain.
```
git commit --amend
```
### Changing Multiple Commit Messages
Agar aapko apne Git history mein peeche ki taraf kisi commit ko modify karna hai, toh aapko thoda complex tools ka istemal karna padega. Git mein koi specific modify-history tool nahi hota, lekin aap rebase tool ka istemal karke commits ka ek series ko HEAD par rebase kar sakte hain.
```
git rebase -i HEAD~3
```
Yahan HEAD~3 ka matlab hai ki aap teen recent commits ko modify karna chahte hain, lekin yeh chaar commits tak ke parents ko designate kar raha hai.
# Git commmit ammend
Aap git commit --amend command se commit message ko badal sakte hain. Jab aap changes kar lein, to git rebase --continue command chalayen:
```
$ git commit --amend
$ git rebase --continue
```
- Use amend for quick fixes on the last commit, and rebase -i for more detailed changes across multiple commits.
# Squashing Commits
Agar tum multiple commits ko ek single commit mein squash karna chahte ho, to interactive rebase ka use kar sakte ho. Rebase message mein helpful instructions hoti hain, jaise:
```
git rebase -i HEAD~3
pick f7f3f6d Change my name a bit
squash 310154e Update README formatting and add blame
squash a5f4a0d Add cat-file
```
iske liye aap emac editor ka use kar sakte hai. jab editor open hoga tab app pick option par click krke upr ki taraf rebase ka option hota hai usme se aap squash option select kar sakte hai.iske baad new editor open hoga jisme aap combine commits ka new commit name de sakte hai.
# Splitting Commits
Splitting a commit in Git ka matlab hai ek commit ko multiple commits mein todna. Agar aapko ek commit ko do ya zyada commits mein todna hai, toh aap rebase -i (interactive rebase) ka use kar sakte ho. Jaise, maan lo aapke paas 3 commits hain, aur beech wale commit ko do parts mein todna hai. Us commit ko "edit" mein change karo rebase script mein:
```
pick f7f3f6d Change my name a bit  
edit 310154e Update README formatting and add blame  
pick a5f4a0d Add cat-file
```
Jab tum script save karke exit karoge, Git tumhe command line pe le aayega. Ab tum is commit ka mixed reset karoge taaki wo changes unstaged ho jaayein:
```
$ git reset HEAD^
```
Iske baad tum apne desired cha
nges ko stage karke commit karoge. Maan lo pehle tum README ko stage karte ho aur commit karte ho:
```
$ git add README  
$ git commit -m 'Update README formatting'
```
Phir tum doosra file stage karke doosra commit banate ho:
```
$ git add lib/simplegit.rb  
$ git commit -m 'Add blame'
```
Phir tum doosra file stage karke doosra commit banate ho:
```
$ git add lib/simplegit.rb  
$ git commit -m 'Add blame'
```
Jab tum yeh sab commits kar loge, tab tum git rebase --continue chalaoge:
```
$ git rebase --continue
```
Deleting a commit
Agar tumhe koi commit delete karna hai, toh tum rebase -i ka use karke us commit ko hata sakte ho. Yaha steps diye gaye hain jo tum follow kar sakte ho:
```
git rebase -i 
```
jab aapka emac editor open hoga tab aapko commit pr pointer ko lejana hai and then rebase option pe click krke aap kill option select kar sakte hai. editor ko save kar sakte hai isse aapki comit delete ho jayegi.but yaha single koi ek commit bachi hai to vo delete nahi hoti.
# Changing Email Address Globally in Commits
Agar aapko apne purane commits ke email address ko change karna hai, to git filter-branch ka use kar sakte ho. Maan lo ki aapka email schacon@localhost hai aur aap usse change karna chahte ho. Yeh command aapke purane email ko naye email ke sath replace karegi:
```
git filter-branch --commit-filter '
    if [ "$GIT_AUTHOR_EMAIL" = "schacon@localhost" ]; 
    then 
        GIT_AUTHOR_NAME="Scott Chacon";
        GIT_AUTHOR_EMAIL="schacon@example.com";
        git commit-tree "$@";
    else
        git commit-tree "$@";
    fi' HEAD
```
# Subdirectory Ko Root Banana

Maan lo aapne kisi dusre source control system se import kiya hai, aur aapke paas kuch bekaar subdirectories hain (jaise trunk, tags, etc.). Agar aap trunk subdirectory ko project ka naya root banana chahte ho, to filter-branch use kar sakte ho:

```
git filter-branch --subdirectory-filter trunk HEAD
```
# Reset Simplified
Git mein reset aur checkout commands pehle thodi confusing lagti hain, lekin hum ise easy words me samajh sakte hain.
- HEAD: Yeh aapka last commit snapshot hai, jo agle commit ka parent hoga.
- Index (Staging Area): Yeh aapke next commit ka proposed snapshot hai. Jo files stage hui hain, unhe commit karne se pehle yahan dekha ja sakta hai.
- Working Directory: Yeh sandbox hai jahan aap files ko real-time edit karte ho. Commit karne se pehle aap apne changes ko yahan check kar sakte ho.
## Reset to a Specific Commit
Aap apne branch ko ek specific commit par reset kar sakte hain, jo aapko kuch commits ko discard karne ka option deta hai:

   - Soft Reset: Isme aapke changes staging area mein safe rehte hain.
    ```
    git reset --soft <commit>
    ```
    Yeh tab useful hota hai jab aap apne pichle kuch commits ko change karna chahte hain bina apna kaam khoe.

   - Mixed Reset (default): Isme aapke changes working directory mein rehte hain, par unhe unstaged kar diya jata hai.
     ```
     git reset <commit>
     ```
     Yeh default behavior hai aur isse aap commit ko undo kar sakte hain, lekin changes ko safe rakhe rehta hai.

     - Hard Reset: Isme working directory aur staging area ke saare changes ko discard kar diya jata hai.
     ```
     git reset --hard <commit>
     ```
     Yeh ek destructive command hai jo specified commit ke baad ke saare changes ko delete kar deta hai.
     # Changes Ko Completely Discard Karna
     Agar aapke paas uncommitted changes hain aur aap unhe poori tarah se discard karna chahte hain, to aap yeh command use kar sakte hain:
     ```
     git reset --hard HEAD
     ```
     Yeh aapki working directory aur staging area ko last commit par reset kar dega, aur effectively sabhi changes ko discard kar dega.
# Advanced Merging
Git mein merging kaafi aasaan hoti hai. Kyunki Git mein aap multiple times doosri branch ko merge kar sakte ho, iska matlab aap long-lived branch rakh sakte ho, aur beech mein update karte raho, chhote chhote conflicts solve karte raho, instead of ek bade conflict ka end mein samna karne se.
## Merge Conflicts
Basic merge conflicts ko resolve karne ke baad, complex conflicts ke liye Git kuch tools provide karta hai jo aapko samajhne mein help karte hain ki kya ho raha hai aur kaise deal karna hai.

  -  Kaam Clean Karo: Pehle, agar possible ho to ensure karo ki aapka working directory clean ho before merge. Agar aapko lagta hai ki conflicts ho sakte hain, toh apne kaam ko temporary branch mein commit ya stash karo, taki kuch galat ho to aap easily wapas aa sako.

   -  Merge Abort Karna : Agar aap conflicts nahi expect kar rahe the aur abhi resolve nahi karna chahte, to git merge --abort se merge ko back out kar sakte ho. Ye aapko merge ke pehle waale state mein wapas le aayega.
     
 ```
git merge --abort
```

- Ignoring Whitespace : Agar conflicts sirf whitespace related hain, to aap merge ko abort kar ke, phir se merge kar sakte ho using -Xignore-all-space ya -Xignore-space-change option ke sath. Ye options whitespace ko ignore karte hain jab files compare ki jaati hain.
  
```
$ git merge -Xignore-space-change <branch name>
```
# Our or Theirs Preference
Yeh concept samjhane ke liye main use karunga simple example jisme hum Git merging ke baare mein discuss kar rahe hain.

By default, jab Git kisi conflict ko detect karta hai jab aap do branches ko merge karte ho, to yeh aapko conflict markers (jaise <<<<<<, =======, >>>>>>) code mein daal deta hai aur aapko manually resolve karne ke liye kehata hai. Lekin agar aap chahte ho ki Git ek particular side ko choose kare aur doosre side ko ignore kare bina aapse puchhe, to aap -Xours ya -Xtheirs option use kar sakte ho merge command ke sath.
Difference between -Xours and -Xtheirs

- Xours: Jab conflict aata hai, current branch (jo branch pe aap ho) ko choose karta hai aur doosre branch ke changes ko ignore karta hai.
- Xtheirs: Isme aap jo doosri branch merge kar rahe ho (jaise mundo), uske changes ko accept karega aur current branch ke changes ko ignore karega.

Example ke taur par, maan lo aap master branch pe ho aur aap mundo branch ko merge kar rahe ho, lekin aap chahte ho ki agar koi conflict aata hai to master branch ke changes automatically retain ho jayein. Us case mein, aap yeh command use kar sakte ho:
```
$ git merge -Xours mundo
```
Iska fayda yeh hoga ki bina conflict markers ke Git master ke changes rakh lega, lekin jo non-conflicting changes hain mundo branch ke, unhe merge kar lega.

Lekin agar aap doosre side ke changes rakhna chahte ho, to aap -Xtheirs use karoge:
```
$ git merge -Xtheirs mundo
```
Yeh ensure karega ki mundo branch ke changes rakhe jayein aur master branch ke conflicted changes ignore ho jayein.
### “Ours” Merge Strategy

-Xours aur -Xtheirs se alag, ek aur option hota hai -s ours. Yeh ek fake merge strategy hoti hai jo sirf aapke current branch ke changes ko rakhti hai bina doosre branch ke changes ko dekh kar. Yeh command kuch aisa hota hai:
```
$ git merge -s ours mundo
```
# Rerere
Git ka rerere feature ek kaafi useful aur thoda hidden functionality hai. Rerere ka full form hai "reuse recorded resolution". Iska kaam yeh hota hai ki jab aap ek merge conflict ko manually resolve karte ho, to Git uss resolution ko yaad rakhta hai, taaki agar future mein wahi conflict firse aata hai, to Git automatically usko resolve kar sake bina aapse dobara manual intervention ke.
# Steps to Use rerere in Git
## Enable rerere

Pehle rerere feature ko enable karna hoga. Aap global level pe ya specific repository ke liye enable kar sakte ho.

- Globally enable:
  ```
  git config --global rerere.enabled true
  ```
 ### Per repository enable:
 Yeh command globally ya local repository ke liye rerere feature ko activate kar dega.
 ```
git config rerere.enabled true
 ```
### Encounter a Conflict

Aap jab kisi branch ko merge kar rahe ho ya rebase kar rahe ho, aur ek conflict aata hai, Git conflict ko detect karega.
```
git merge feature-branch
```
### Resolve the Conflict Manually

Jaise aap normal merge conflicts ko resolve karte ho, ussi tarah aap manually conflict resolve karenge.
Edit the conflicted file
```
vim hello.rb
```
Resolve karne ke baad, file ko stage kar dein aur commit kar dein.
```
git add hello.rb
git commit
```
### rerere Records the Resolution
Jab aapne conflict resolve kiya aur commit kiya, rerere uss resolution ko automatically yaad rakh lega. Aap isko manually track kar sakte ho:
```
git rerere status
```
Agar future mein same file ya branch mein dubara wahi conflict aata hai, to rerere automatically usko resolve kar dega bina aapse manually resolve karne ko kahe.
### Undo a Conflict Resolution
Agar aap ek conflict ko resolve kar chuke ho, lekin aap wapas jaake resolve ko undo karna chahte ho, aap use kar sakte ho:
```
git rerere forget
```
Yeh command conflict resolution ko forget kar dega taaki aap manually dobara resolve kar sakein.

# Debugging with Git

Git sirf version control ke liye hi nahi, balki aapke source code projects ko debug karne mein bhi madad karta hai. Git aise kai commands provide karta hai jo generic hain, lekin aksar bugs ya issues trace karne mein bahut useful sabit hote hain.
Example: git blame ka use karke commit aur committer identify karna
```
$ git blame -L 69,82 Makefile
```
- Special Notation:

    ^1da177e4c3f4: Yeh indicate karta hai ki yeh lines repository ke initial commit mein introduce hui thi aur uske baad se kabhi change nahi hui hain. Git mein ^ prefix ka matlab alag-alag context mein thoda confusing ho sakta hai, lekin yahan yeh sirf reference hai.
#  Binary Search in Git
Agar tumhe nahi pata ki bug kaha hai, aur kayi commits ho chuke hain since the last known working state, toh tum git bisect ka use kar sakte ho. git bisect ek binary search karta hai tumhare commit history mein taaki jaldi se pata chale ki issue kis commit se introduce hua.
- Start Bisect:
  Sabse pehle, tum git bisect start chalate ho, jo bisecting process ko shuru karta hai.
  Fir, tum Git ko current commit ke baare mein bataoge ki yeh "bura" (bad) hai, yani is commit mein bug hai.
```
git bisect start
git bisect bad
```
- Last Known Good Commit Batana:
Uske baad, tumhe ek commit specify karna hoga jisme bug nahi tha, yani wo achha (good) commit hai. Tum git log ya git reflog ka use karke yeh sha-1 commit hash pata kar sakte ho.
```
git bisect good <achha_commit>
```
git bisect run ke sath hum ek script (test-error.sh) ko run karvate hain jo har commit ko check karta hai aur decide karta hai ki bug present hai ya nahi.
```
$ git bisect run <script-name>
```
# Submodules
Jab aap kisi project mein kaam kar rahe hote ho aur usmein doosre project ki zaroorat hoti hai, toh aapko submodules ka use karna padta hai. Ye tab helpful hota hai jab aap ek library ya code ka part apne project mein include karte ho, jo kisi aur ne develop kiya ho ya aap alag se bana rahe ho aur multiple parent projects mein use karna ho.

- Example se samjhte hain:
Suppose aap ek website develop kar rahe ho jisme aap Atom feeds generate karna chahte ho. Iske liye aap apna khud ka Atom generator code likhne ke bajaye koi existing library use karna prefer karte ho. Aapko ya toh library ko apne project mein copy karna padta ya phir kisi package manager (jaise CPAN ya Ruby gem) se install karna padta. Copy karne se ye dikkat hoti hai ki jab library update hoti hai toh merge karna mushkil hota hai, aur include karne se ye problem aati hai ki har client ko library available karani padti hai.

Is problem ko Git submodules se solve karta hai. Submodules allow karte hain ki ek Git repository ko doosre Git repository ke andar subdirectory ki tarah rakha ja sake. Aap doosre repository ko apne project mein clone kar sakte ho aur uske commits ko alag se track kar sakte ho.
## Submodules add karna:
```
$ git submodule add https://github.com/chaconinc/DbConnector
```
Commit karne par kuch aisa dikhai dega:
```
$ git commit -am 'Add DbConnector module'
[master fb9093c] Add DbConnector module
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 DbConnector
```
Notice karo 160000 mode jo ek special mode hai Git mein, ye batata hai ki ek commit ko directory ke form mein record kiya gaya hai, file ya subdirectory ke form mein nahi.
- Submodule wala project clone karna:
Jab aap ek project clone karte ho jisme submodule ho, toh by default aapko sirf wo directories milti hain jisme submodules hain, lekin un directories ke andar koi files nahi hoti.
```
$ git clone https://github.com/chaconinc/MainProject
$ git submodule update --init
```
Ye last command submodule ke andar ki files bhi pull kar legi aur sab kuch sync ho jayega.

Aap ek aur simpler tareeke se submodule ko clone kar sakte ho. Agar aap --recurse-submodules option ko git clone command ke sath pass karte ho, toh ye automatically har submodule ko initialize aur update kar dega, chahe wo nested submodules ho ya simple.
```
$ git clone --recurse-submodules https://github.com/chaconinc/MainProject
```
Agar aapko check karna hai ki koi naye updates hai kya submodule me, toh aap submodule ki directory me jaake git fetch aur git merge run kar sakte ho:
```
$ git fetch
From https://github.com/chaconinc/DbConnector  
c3f01dc..d0354fc  master -> origin/master
$ git merge origin/master
Updating c3f01dc..d0354fc
Fast-forward
 scripts/connect.sh | 1 +
 src/db.c           | 1 +
 2 files changed, 2 insertions(+)
```
Ye commands submodule ke latest changes ko aapki local copy me merge kar deti hain.
Easy way to update submodules:
```
$ git submodule update --remote
```
Agar aap manually subdirectory me fetch aur merge nahi karna chahte, toh aap git submodule update --remote command run kar sakte ho. Ye command automatically submodules me jaake fetch aur update kar degi.


Agar aap submodule ke branch ko track karna chahte ho, toh git config -f .gitmodules submodule.<name>.branch <branch> ka use karte ho. Example me, hum DbConnector submodule ko stable branch par track kar rahe hain.
```
$ git config -f .gitmodules submodule.DbConnector.branch stable
$ git submodule update --remote
```
$ git log -p --submodule, submodule me kaunse naye commits aa rahe hain. Commit karne ke baad aap git log -p --submodule run karke bhi yeh information dekh sakte ho.
```
$ git log -p --submodule
```
## Submodule Tips

Submodules ko handle karna easy banane ke liye kuch tips hai.

Submodule Foreach: foreach command submodule mein koi bhi arbitrary command run karne ke liye helpful hoti hai. Agar same project mein multiple submodules ho, toh ye useful hota hai.
```
$ git submodule foreach 'git stash'
```
- Useful Aliases: Aap kuch useful aliases setup kar sakte ho jo long commands ko shortcut mein convert karein. Example:
```
$ git config alias.sdiff '!'"git diff && git submodule foreach 'git diff'"
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge'
```

Here's the translation of the provided content into Hinglish, along with the main points that can be highlighted for a document:

# Bundling
Bundling ka Parichay: Humne Git data ko network par transfer karne ke common tarike (HTTP, SSH, etc.) ke baare mein baat ki hai, lekin ek aur tarika hai jo aam taur par use nahi hota lekin kaafi useful ho sakta hai. Git apne data ko ek single file mein "bundle" karne ki kshamata rakhta hai. Ye kayi scenarios mein kaam aa sakta hai, jaise:

- Jab aapka network down hai aur aap apne co-workers ko changes bhejna chahte hain.
- Jab aap kahin offsite hain aur local network tak access nahi hai.
- Jab aapka wireless/ethernet card kharab ho gaya ho.
- Jab aapke paas shared server tak access nahi hai aur aap kisi ko updates email karna chahte hain bina 40 commits ko transfer kiye.
- Git Bundle Command: Yahaan git bundle command madadgar ho sakti hai. Ye command saara data jo aam taur par git push command ke sath transfer hota hai, ek binary file mein package kar deti hai, - jise aap kisi ko email kar sakte hain ya flash drive par rakh sakte hain, phir ise dusre repository mein unbundle kar sakte hain.

aap repository ko kisi ko bhejna chahte toh aap isse git bundle create se bundle kar sakte hain:
```
$ git bundle create repo.bundle HEAD master
```
Bundle ko Email ya USB Se Transfer Karna: Aap is repo.bundle file ko kisi ko email kar sakte hain, ya ise USB drive par rakh kar le ja sakte hain. Dusri taraf, agar aapko ye repo.bundle file mile aur aap project par kaam karna chahte hain, toh aap is binary file se directory mein clone kar sakte hain:
```
$ git clone repo.bundle repo
```
Bundle Verification: Jab wo bundle ko receive karti hain, toh wo ise inspect kar sakti hain ye dekhne ke liye ki isme kya hai. Pehla command bundle verify hota hai jo ye confirm karega ki file sach mein ek valid Git bundle hai aur aapke paas usse sahi tarike se recreate karne ke liye zaroori ancestors hain:
```
$ git bundle verify ../commits.bundle
```
# Replace
Replace ka Parichay: Git mein objects ko replace karne ka ek tarika hai jisse aap kisi object ko dusre object se replace kar sakte hain bina history ko modify kiye. Ye kaafi useful hai jab aap ek commit ko dusre commit se replace karna chahte hain.

Example Scenario: Agar aapke paas ek bada code history hai aur aap isse do parts mein split karna chahte hain, jaise ek short history naye developers ke liye aur ek long history data mining ke liye, toh aap replace command ka istemal kar sakte hain.

Steps:
```
$ git log --oneline
ef989d8 Fifth commit
c6e1e95 Fourth commit
9c68fdc Third commit
945704c Second commit
c1822cf First commit
```
Historical History Banana:
```
$ git branch history c6e1e95
$ git remote add project-history https://github.com/schacon/project-history
$ git push project-history history:master
```
Recent History ko Chhota Karna:
```
$ git log --oneline --decorate
```
Base Commit Banana:
```
$ echo 'Get history from blah blah blah' | git commit-tree 9c68fdc^{tree}
```
Plumbing Commands: commit-tree command ko plumbing commands kaha jaata hai, jo low-level tasks ke liye istemal hoti hain.
