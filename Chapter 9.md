# Git Internals
Yeh chapter Git ke internal kaam ko samjhata hai.
Sabse pehle, yeh samajhna zaroori hai ki Git ek content-addressable filesystem hai jiske upar ek Version Control System (VCS) user interface likha gaya hai. Iska matlab yeh hai ki Git ka base structure ek aise filesystem par depend karta hai jisme content ko address ya identify kiya jaata hai unke unique hash values se.
## Content-Addressable Filesystem kya hota hai?
Jab aap Git me koi file save karte ho ya commit banate ho, Git us content ko ek unique hash value (SHA-1) ke through store karta hai. Matlab aapke file ka content hi uska address ban jaata hai, aur har unique content ka ek unique hash hoga.

Pehle Git ka user interface kaafi complex tha, especially v1.5 se pehle, kyunki us waqt zyada focus Git ke filesystem layer par tha. Aaj kal, Git ka UI kaafi refine ho chuka hai, lekin pehle ki uski complicated reputation ab tak logon ke dimaag me hai.

Is chapter mein, hum pehle yeh content-addressable filesystem samjhenge, aur phir transport mechanisms aur repository maintenance ke baare mein padhenge jo kabhi kabhi zaroori ho sakti hain.
Plumbing and Porcelain
Git ke commands do categories mein divide hote hain: plumbing aur porcelain.

### Porcelain Commands
Yeh wo commands hain jo user-friendly hoti hain, jaise checkout, branch, remote, etc. Aap inhe direct use karte ho apne daily work ke liye, aur book ke pehle 9 chapters mein zyada tar porcelain commands ko hi cover kiya gaya hai.

### Plumbing Commands
Yeh commands low-level operations ke liye hoti hain, jo zyada tar scripts ya tools banane ke liye use ki jati hain. Inhe manually use karna zaroori nahi hota, lekin yeh commands Git ke internal workings ko samjhne ke liye helpful hoti hain. Plumbing commands ko chain kar ke UNIX style mein ya custom scripts mein use kiya jaata hai.

Jab aap git init command chalate ho, toh Git ek .git directory create karta hai. Is directory ke andar hi Git ki sari information store hoti hai. Agar aap apna repository backup karna chahein, toh .git folder copy kar lena kaafi hota hai.
# Git Objects

Git ek content-addressable filesystem hai, iska matlab hai ki Git ek simple key-value data store system ke tarah kaam karta hai. Jab aap koi content Git repository mein store karte ho, to Git aapko ek unique key (SHA-1 hash) deta hai, jise aap baad mein us content ko retrieve karne ke liye use kar sakte ho.

Example:
- Pehle ek new Git repository initialize karte hain:
```
$ git init test
$ cd test
```
- Ab git hash-object command use karke ek naya object create karte hain. Yeh command content ko .git/objects folder mein store karta hai aur uska unique key (hash) return karta hai:
```
$ echo 'test content' | git hash-object -w --stdin
d670460b4b4aece5915caf5c68d12f560a9fe3e4
```
-w: Content ko Git database mein store karta hai.
--stdin: Content ko stdin se leta hai (file se nahi).
- Ab yeh content Git ki object database mein store ho gaya hai. Aap check kar sakte ho:
```
$ find .git/objects -type f
.git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4
```
Agar aap yeh content dekhna chahein, toh git cat-file -p use kar sakte ho:
```
$ git cat-file -p d670460b4b4aece5915caf5c68d12f560a9fe3e4
test content
```
Aap file mein kuch versioning bhi kar sakte ho. Pehle ek file create karo aur uska object store karo:
```
$ echo 'version 1' > test.txt
$ git hash-object -w test.txt
83baae61804e65cc73a7201a7252750c76066a30
```
- Phir file mein kuch change karo aur naya version store karo:
```
$ echo 'version 2' > test.txt
$ git hash-object -w test.txt
1f7a7a472abf3dd9643fd615f6da379c4acb3e3a
```
Aap purani versions ko bhi retrieve kar sakte ho:

Version 1:
```
$ git cat-file -p 83baae61804e65cc73a7201a7252750c76066a30 > test.txt
$ cat test.txt
version 1
```
Version 2:
```
$ git cat-file -p 1f7a7a472abf3dd9643fd615f6da379c4acb3e3a > test.txt
$ cat test.txt
version 2
```
Blob ek object type hai jo Git mein content ko represent karta hai, aur har object ek SHA-1 hash key ke sath store hota hai.
