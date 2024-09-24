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

