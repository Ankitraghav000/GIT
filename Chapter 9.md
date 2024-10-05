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
# Git References
Jab aap command $ cat .git/HEAD chalate ho, aapko jo ref milega, vo batata hai ki aap kis branch pe ho. Jaise agar refs/heads/test dikh raha hai, iska matlab hai ki aap "test" branch pe ho.

Jab aap git commit karte ho, to vo commit object banata hai aur uske parent ko us commit ka SHA-1 value assign karta hai jo HEAD point kar raha hota hai.

Aap manually bhi .git/HEAD file ko edit kar sakte ho, lekin safer tarika hai git symbolic-ref command use karna. Jaise:
```
$ git symbolic-ref HEAD refs/heads/master
```
Yeh command aapko HEAD ki value read karne aur set karne me help karti hai.

## Tags:
Git me teen main object types hain: blob, tree, aur commit. Lekin ek fourth object bhi hota hai, jo hai tag object. Yeh commit object ki tarah hota hai, but yeh usually kisi commit ko point karta hai. Tag reference kabhi move nahi hota, aur commit ko ek friendly name deta hai.

Tags do types ke hote hain:

- Lightweight tag: Yeh ek simple reference hota hai jo kabhi change nahi hota.

```
$ git update-ref refs/tags/v1.0 <commit-hash>
```
Annotated tag: Isme extra details hoti hain jaise message aur date.
```
$ git tag -a v1.1 <commit-hash> -m 'Test tag'
```
Example ke liye, agar aap git cat-file -p chalate ho kisi tag SHA-1 ke upar, to aapko object ke details milenge.

## References:
References ya "refs" Git me simple names hote hain jo commits ko point karte hain. Yeh .git/refs directory me store hote hain.

Agar aap ek new reference banana chahte ho, to aap simple command se commit ko ek naam de sakte ho:
```
$ echo <commit-hash> > .git/refs/heads/ master
```
To check who is root
```
git log --max-parents=0 --pretty=format:"%H - %an - %ae - %ad"
```
Aap git update-ref command use kar ke references ko safely update kar sakte ho.
# Packfiles

Agar aapne pichle section ke example ki sabhi instructions follow ki hain, toh ab aapke paas ek test Git repository hona chahiye jismein 11 objects honge — 4 blobs, 3 trees, 3 commits, aur 1 tag:
```
$ find .git/objects -type f
.git/objects/01/55eb4229851634a0f03eb265b69f5a2d56f341    # tree 2
.git/objects/1a/410efbd13591db07496601ebc7a059dd55cfe9    # commit 3
.git/objects/1f/7a7a472abf3dd9643fd615f6da379c4acb3e3a    # test.txt v2
.git/objects/3c/4e9cd789d88d8d89c1073707c3585e41b0e614    # tree 3
.git/objects/83/baae61804e65cc73a7201a7252750c76066a30    # test.txt v1
.git/objects/95/85191f37f7b0fb9444f35a9bf50de191beadc2    # tag
.git/objects/ca/c0cab538b970a37ea1e769cbbde608743bc96d    # commit 2
.git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4    # 'test content'
.git/objects/d8/329fc1cc938780ffdd9f94e0d364e0ea74f579    # tree 1
.git/objects/fa/49b077972391ad58037050f2a75f74e3671e92    # new.txt
.git/objects/fd/f4fc3344e67ab068f836878b6c4951e3b15f3d    # commit 1
```
Git in files ka content zlib se compress karta hai, aur aap jyada space nahi le rahe, toh ye sab files collectively sirf 925 bytes ka space leti hain. Ab aap repository mein kuch bada content add karenge taaki Git ke ek interesting feature ko demonstrate kar sakein.

Demonstrate karne ke liye, hum Grit library ka repo.rb file add karenge — ye ek 22K source code file hai:
```
$ curl https://raw.githubusercontent.com/mojombo/grit/master/lib/grit/repo.rb > repo.rb
$ git checkout master
$ git add repo.rb
$ git commit -m 'Create repo.rb'
```
Output:
```
[master 484a592] Create repo.rb
3 files changed, 709 insertions(+), 2 deletions(-)
delete mode 100644 bak/test.txt
create mode 100644 repo.rb
rewrite test.txt (100%)
```
Agar aap resulting tree dekhen, toh aapko SHA-1 value milegi jo aapke naye repo.rb blob object ke liye calculate hui:
```
$ git cat-file -p master^{tree}
100644 blob fa49b077972391ad58037050f2a75f74e3671e92      new.txt
100644 blob 033b4468fa6b2a9547a70d88d1bbe8bf3f9ed0d5      repo.rb
100644 blob e3f094f522629ae358806b17daf78246c27c007b      test.txt
```
Aap git cat-file ka use karke dekh sakte hain ki wo object kitna bada hai:

```
$ git cat-file -s 033b4468fa6b2a9547a70d88d1bbe8bf3f9ed0d5
22044
```
Is point par, aap file ko thoda modify karein, aur dekhein kya hota hai:
```
$ echo '# testing' >> repo.rb
$ git commit -am 'Modify repo.rb a bit'
```
Output:
```
[master 2431da6] Modify repo.rb a bit
1 file changed, 1 insertion(+)
```
Ab tree ko check karein jo last commit se create hua tha, aur aap kuch interesting dekhenge:
```
$ git cat-file -p master^{tree}
100644 blob fa49b077972391ad58037050f2a75f74e3671e92      new.txt
100644 blob b042a60ef7dff760008df33cee372b945b6e884e      repo.rb
100644 blob e3f094f522629ae358806b17daf78246c27c007b      test.txt
```
Ab blob ek naya blob hai, iska matlab yeh hai ki halanki aapne sirf ek line file ke last mein add ki thi, Git ne naye content ko ek completely naye object ke roop mein store kiya:
```
$ git cat-file -s b042a60ef7dff760008df33cee372b945b6e884e
22054
```
Aapke disk par ab do lagbhag identical 22K objects hain (har ek approx 7K mein compressed). Kya accha nahi hota agar Git ek ko poori tarah se store karta aur doosre object ko sirf pehle aur doosre ke beech ke difference ke roop mein store karta?

Actually, Git yeh kar sakta hai. Git initially objects ko "loose" object format mein disk par save karta hai. Lekin kabhi-kabhi Git in objects ko ek single binary file mein pack kar deta hai jise "packfile" kehte hain, taaki space bache aur efficiency bade. Git yeh tab karta hai jab aapke paas bohot saare loose objects hote hain, ya aap manually git gc command run karte hain, ya jab aap remote server pe push karte hain.

Aap manually git gc run karke objects ko pack karne ko bol sakte hain:
```
$ git gc
Counting objects: 18, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (14/14), done.
Writing objects: 100% (18/18), done.
Total 18 (delta 3), reused 0 (delta 0)
```
Agar aap apne objects directory mein dekhein, toh aap dekhenge ki jyadatar objects gayab hain, aur naye files ka ek pair aa gaya hai:
```
$ find .git/objects -type f
.git/objects/bd/9dbf5aae1a3862dd1526723246b20206e5fc37
.git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4
.git/objects/info/packs
.git/objects/pack/pack-978e03944f5c581011e6998cd0e9e30000905586.idx
.git/objects/pack/pack-978e03944f5c581011e6998cd0e9e30000905586.pack
```
Jo objects bache hain, wo blobs hain jo kisi commit se point nahi hote — is case mein, "what is up, doc?" example aur "test content" example blobs jo aapne pehle create kiye the. Kyunki aapne inhe kabhi kisi commit mein add nahi kiya, ye dangling maane jaate hain aur aapke naye packfile mein pack nahi hote.

Baaki files aapka naya packfile aur ek index hain. Packfile ek single file hoti hai jo un objects ka content contain karti hai jo aapke file system se remove kiye gaye the. Index ek file hoti hai jo packfile mein specific object ko quickly find karne ke liye offsets contain karti hai. Jo cheez interesting hai wo yeh hai ki objects jo disk pe pehle 15K size mein the, naye packfile mein sirf 7K space le rahe hain. Aapne packing karke apni disk usage aadhi kar di hai.

Git yeh kaise karta hai? Jab Git objects ko pack karta hai, toh wo same naam aur size waale files ko dhundta hai, aur unhe bas deltas ke roop mein store karta hai ek version se doosre version tak. Aap packfile ke andar dekh sakte hain ki Git ne kaise space save kiya. git verify-pack plumbing command aapko dikhane mein madad karta hai ki kya pack hua tha:
```
$ git verify-pack -v .git/objects/pack/pack-978e03944f5c581011e6998cd0e9e30000905586.idx
```
Yaha, 033b4 blob, jo aapke pehle repo.rb file ka version tha, ab b042a blob ko reference kar raha hai, jo file ka doosra version tha. Teesra column object ka pack mein size hai, toh aap dekh sakte hain ki b042a 22K file space le raha hai, lekin 033b4 sirf 9 bytes ka space le raha hai. Jo interesting baat hai

# The Refspec
Refspec Git ka ek pattern hota hai jo batata hai ki remote branches ko local branches ke sath kaise map karna hai. Ye fetch aur push commands ke sath kaam karta hai.

Example: Remote Add
Jab tum remote add karte ho, jaise:
```
$ git remote add origin https://github.com/user/repo.git
```
Toh .git/config file mein kuch aisa add ho jata hai:
```
[remote "origin"]
    url = https://github.com/user/repo.git
    fetch = +refs/heads/*:refs/remotes/origin/*
fetch = +refs/heads/*:refs/remotes/origin/*
```
Iska matlab hai ki remote ke saare branches ko refs/remotes/origin/ mein fetch karenge.
One-Time Fetch Example:
Agar tum remote master branch ko local mymaster branch ke sath fetch karna chahte ho:
```
$ git fetch origin master:refs/remotes/origin/mymaster
```
Refspec powerful tool hai Git mein jo fetching aur pushing processes ko customize karta hai. Isse tum specific branches ya namespaces ka achhe tareeke se management kar sakte ho.

Push Refspec Example:
Agar tum local master branch ko remote qa/master branch pe push karna chahte ho:
```
$ git push origin master:refs/heads/qa/master
```
