# GIT
Yahaan aapko Git ke baare mein chapter-by-chapter samjhaaya jaayega. Har chapter Git ke kisi na kisi important concept ko simple aur easy language mein explain karega.
# Getting Started 
Yeh chapter Git ke saath shuru karne ke baare mein hoga. Hum pehle version control tools ke background ke baare mein samjhenge, phir Git ko apne system par kaise install karna hai, aur kaise kaam shuru karne ke liye setup karna hai. Is chapter ke ant mein aap samajh jayenge ki Git kyun zaroori hai, aapko isse kyun use karna chahiye, aur aap ready honge isse istemal karne ke liye.

Version Control ke baare mein Version control kya hota hai aur aapko iski zaroorat kyun hai? Version control ek aisi system hai jo kisi file ya file set par samay ke saath hone wale changes ko record karta hai, taaki aap specific versions ko baad mein recall kar sakein. Iss book ke examples mein hum software source code ka use karenge, lekin aap computer par kisi bhi type ki file ka version control kar sakte hain.

Agar aap ek graphic ya web designer hain aur aapko kisi image ya layout ke sabhi versions ko save karna hai, toh Version Control System (VCS) ka istemal ek wise choice hai. Yeh aapko files ko pichle state mein revert karne, puri project ko wapas pichle state mein lane, changes ko samay ke saath compare karne, aur kisne kya modify kiya yeh dekhne mein madad karta hai. VCS use karne ka ek aur fayda yeh hai ki agar kuch galat ho jaye ya files kho jayein, toh aap asani se recover kar sakte hain.

## Local Version Control Systems
Bohot log files ko alag directory mein copy kar ke version control karte hain, lekin yeh method galtiyon se bhara hota hai. Is issue ko solve karne ke liye, local VCS develop kiye gaye jo ek simple database mein files ke changes ko record karte hain.

## Centralized Version Control Systems (CVCS)
Jab logo ko different systems par kaam karte hue collaborate karna hota hai, toh Centralized Version Control Systems ka istemal kiya jata hai. CVCS ek central server par sabhi versioned files ko rakhta hai aur users files ko wahaan se check out karte hain. Lekin iska ek major drawback yeh hai ki agar server fail ho jaye, toh pura project history kho sakte hain.
![vcs](https://github.com/user-attachments/assets/5e0e8dda-c5d7-4a66-a9a1-e46269f5120e)


## Distributed Version Control Systems (DVCS)
Distributed Version Control Systems (jaise Git, Mercurial) mein har client ke paas repository ka full history hota hai. Agar koi server fail ho jaye, toh client repositories se data recover kiya ja sakta hai. Is system mein aap simultaneously alag-alag groups ke saath kaam kar sakte hain aur hierarchical workflows bhi set kar sakte hain jo centralized systems mein possible nahi hote.

## Git ki Short History
Git ka shuruat ek controversy ke saath hui. Linux kernel ek open source software project hai. 1991 se 2002 tak, changes patches aur archived files ke roop mein distribute kiye jate the. 2002 mein Linux kernel project ne BitKeeper naam ka proprietary DVCS use karna shuru kiya. 2005 mein BitKeeper ka free status khatam ho gaya aur Linus Torvalds ne apna tool banaya jisse Git ka janm hua. Git ka goal tha speed, simple design, non-linear development, aur distributed system ko support karna.Git Mein Integrity Hoti Hai
Git mein har file checksummed hoti hai aur usse uske unique SHA-1 hash ke through store kiya jaata hai. Is wajah se, bina Git ko pata chale, koi file badli nahi ja sakti. Hash se files ka tracking hota hai, jo integrity maintain karta hai.

2005 ke baad se, Git evolve aur mature hua hai, lekin apne initial qualities ko retain kiya hai. Yeh bohot fast hai, large projects ke liye efficient hai, aur branching system bohot strong hai
## Git kya hai:
Git ek Version Control System (VCS) hai jo files ka record rakhta hai aur unke changes ko track karta hai. Yeh doosre VCSs jaise CVS, Subversion, ya Perforce se alag hai kyunki Git information ko ek unique tarike se store karta hai. Isliye, agar aap Git seekhte waqt purane systems ke concepts ko hata kar samjhenge, toh aapko confusion kam hoga aur Git ko effectively use karna aasan hoga
# Git Mein Integrity Hoti Hai
Git mein har file checksummed hoti hai aur usse uske unique SHA-1 hash ke through store kiya jaata hai. Is wajah se, bina Git ko pata chale, koi file badli nahi ja sakti. Hash se files ka tracking hoti hai, jo integrity maintain karta hai.
The Three States (Hinglish mein):

Git mein aapke files teen main states mein ho sakti hain: modified, staged, aur committed:

- Modified: Jab aapne file ko change kiya hai lekin abhi tak commit nahi kiya.
- Staged: Aapne modified file ko next commit ke liye mark kiya hai.
- Committed: Data aapke local database mein safely store ho gaya hai.
## The Command Line

Git ko use karne ke bahut tareeke hain. Ek hai original command-line tools ka istemal, aur doosra graphical user interfaces (GUIs) ka use karna. Is book mein hum command line pe Git ka use karenge. Command line pe aap saare Git commands run kar sakte ho, jabki GUIs mein sirf limited functionalities hoti hain. 
