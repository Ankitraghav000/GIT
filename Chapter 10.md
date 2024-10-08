# Graphical Interfaces
Git ka main environment terminal hai. Naye features pehle command line par aate hain, aur sirf command line par aapko Git ka pura power milta hai. Lekin har kaam ke liye plain text best nahi hota; kabhi-kabhi aapko visual representation chahiye hota hai, aur kuch users point-and-click interface mein zyada comfortable hote hain.

Yeh samajhna zaroori hai ki alag-alag interfaces alag-alag workflows ke liye banaye gaye hain. Kuch clients sirf carefully selected Git functions ko expose karte hain taaki ek specific tarike ka workflow support kiya ja sake. Is context mein, koi bhi tool “best” nahi hai, balki har ek apne intended purpose ke liye zyada suitable hai. Yeh bhi yaad rakhein ki koi graphical client aapko woh nahi de sakta jo command-line de sakta hai; command-line par aapko sabse zyada control aur power milta hai jab aap apne repositories ke sath kaam karte hain.

- gitk aur git-gui
Jab aap Git install karte hain, toh aapko uske visual tools bhi milte hain, jaise gitk aur git-gui.

gitk ek graphical history viewer hai. Socho ki yeh ek powerful GUI shell hai jo git log aur git grep ka upar ka interface hai. Yeh tool tab kaam aata hai jab aapko dekhna ho ki past mein kya hua tha, ya apne project ka history dekhna ho.

Gitk ko command-line se invoke karna sabse aasaan hai. Bas kisi Git repository mein cd karo, aur type karo:

```
$ gitk [git log options]
``` 
Gitk bohot saare command-line options accept karta hai, jinme se zyadatar git log ke options hote hain. Sabse useful option shayad --all flag hai, jo gitk ko batata hai ki woh kisi bhi ref se reachable commits ko dikhaye, sirf HEAD se nahi. Gitk ka interface kuch aisa dikhai deta hai:

Upar git log --graph ka output jaisa hota hai; har dot ek commit ko represent karta hai, aur lines parent relationships ko show karti hain. Yellow dot HEAD ko dikhata hai, aur red dot un changes ko dikhata hai jo ab tak commit nahi hue. Neeche selected commit ka view hota hai, comments aur patch left side mein, aur summary view right side mein. Beech mein kuch controls hote hain jo history ko search karne mein kaam aate hain.
## Git GUI
git-gui zyada tar crafting commits ke liye use hota hai. Isko bhi command-line se invoke karna aasaan hota hai:
```
$ git gui
```
Iska interface kuch aisa hota hai:

Left side mein index hota hai; unstaged changes upar hoti hain, aur staged changes neeche. Aap poori files ko inn dono states ke beech click karke move kar sakte hain, ya kisi file ko dekhne ke liye uske naam par click kar sakte hain. Top right mein diff view hota hai, jo selected file ke changes dikhata hai. Aap individual hunks (ya individual lines) ko right-click karke stage kar sakte hain. Neeche right mein message aur action area hota hai. Aap apna message text box mein likhte hain aur “Commit” par click karke commit karte hain. Aap last commit ko amend karne ke liye “Amend” radio button bhi select kar sakte hain.

Gitk aur git-gui task-oriented tools ke example hain. Har ek tool ek specific purpose ke liye bana hai (history dekhna aur commits banana), aur us task ke liye zaroori features ko hi dikhata hai.
## Git in Visual Studio
Visual Studio mein Git ka tooling direct IDE ke andar hi bana hua hai, shuru hote hue Visual Studio 2019 version 16.8 se.

Yeh tooling following Git functionalities ko support karti hai:

Repository create ya clone karna.
Repository ka history open aur browse karna.
Branches aur tags create aur checkout karna.
Changes stash, stage, aur commit karna.
Commits fetch, pull, push ya sync karna.
Branches ko merge aur rebase karna.
Merge conflicts resolve karna.
Diffs dekhna.
Aur bhi bohot kuch!
Zyada jaankari ke liye [watch tutorial](https://youtube.com/playlist?list=PLzdlNxYnNoafZq1AKcqiGvj0gkzrjmgq7&si=5YhXAcfv6l3qYTuJ)
