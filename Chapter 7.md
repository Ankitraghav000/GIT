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
jab aap emac editor open hoga tab aapko commit pr pointer ko lejana hai and then rebase option pe click krke aap kill option select kar sakte hai. editor ko save kar sakte hai isse aapki comit delete ho jayegi.but yaha single koi ek commit bachi hai to vo delete nahi hoti.




