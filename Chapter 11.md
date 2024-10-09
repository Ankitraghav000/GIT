# Appendix B:
## Apni Applications mein Git ko Embed karna
Agar aapki application developers ke liye hai, toh chances bohot zyada hain ki source control ke integration ka fayda ho sakta hai. Even non-developer applications, jaise document editors, bhi version-control features se benefit le sakti hain, aur Git ka model kai different scenarios ke liye kaafi achha kaam karta hai.

Agar aapko Git ko apni application ke saath integrate karna hai, toh aapke paas do main options hain: ya toh aap ek shell process chalao aur git command-line program ko call karo, ya phir ek Git library ko apni application mein embed karo. Yahan hum command-line integration aur kuch popular embeddable Git libraries ke baare mein cover karenge.

## Command-line 
Git Ek option yeh hai ki aap ek shell process chalao aur Git command-line tool ko kaam karne do. Iska fayda yeh hai ki  Git ke saare features support karte hain. Yeh kaafi easy bhi hota hai, kyunki zyadatar runtime environments mein command-line arguments ke saath ek process ko invoke karna relatively simple hota hai. Lekin is approach ke kuch downsides bhi hain.
## Libgit2 
ek lightweight, dependency-free library hai jo Git ko implement karti hai. Iska main focus ek achhi API provide karna hai jo doosre programs ke andar Git features ko easily use karne mein help karti hai. Ye Git ka ek low-level implementation hai, jo aapko Git ke functionalities directly access karne ka moka deta hai, bina Git command-line tool ka use kiye.
Example code:

written in c language
```
// Repository ko open karo
git_repository *repo;
int error = git_repository_open(&repo, "/path/to/repository");

// HEAD ko commit se dereference karo
git_object *head_commit;
error = git_revparse_single(&head_commit, repo, "HEAD^{commit}");
git_commit *commit = (git_commit*)head_commit;

// Commit ki properties ko print karo
printf("%s", git_commit_message(commit));
```
Isse Git ke core functions ko aap directly code ke through access kar sakte ho, jo programmatic Git operations ke liye helpful hai.

## Other Bindings
Libgit2 ke bohot saare programming languages mein bindings available hain. Yahaan hum kuch aise examples dekhenge jo complete bindings packages mein hain. C++, Go, Node.js, Erlang, aur JVM jaise aur bhi languages mein bindings exist karti hain, lekin unka development stage alag hota hai. Aap in sab bindings ko https://github.com/libgit2 par dekh sakte ho.

Hum ek example likhenge jo HEAD par point ki gayi commit ka message return karega, jaise ki git log -1 karta hai.

## LibGit2Sharp
Agar aap .NET ya Mono application bana rahe ho, toh aapko LibGit2Sharp (https://github.com/libgit2/libgit2sharp) use karna chahiye. Ye bindings C# mein likhi gayi hain aur Libgit2 calls ko simple aur easy-to-use CLR APIs ke saath wrap kiya gaya hai. Yahaan example code kuch aisa dikhega:

written in csharp
```
new Repository(@"C:\path\to\repo").Head.Tip.Message;
```
Agar aap Windows par desktop applications bana rahe ho, toh aapke liye ek NuGet package bhi available hai jo aapko quickly start karne mein madad karega
## Pygit2
Python ke liye jo Libgit2 bindings hain, unhe Pygit2 kehte hain. Aapko yeh bindings yahaan milengi: https://www.pygit2.org. Yahaan ek chhota sa example program diya hai:

python
```
pygit2.Repository("/path/to/repo")   # repository open karo
   .head                            # current branch fetch karo
   .peel(pygit2.Commit)             # commit tak jao
   .message                         # message read karo
```
Agar aapko Libgit2 ke aur details chahiye, toh aap API documentation yahaan padh sakte ho: https://libgit2.github.com/libgit2, aur guides bhi available hain: https://libgit2.github.com/docs.

Baaki bindings ke liye, unke saath jo README aur tests aaye hain unko zarur dekho, kyunki unmein chhote tutorials ya aur information mil jaayegi.

## JGit
Agar aapko apni Java program mein Git ka use karna hai, toh ek full-featured Git library hai jise JGit kehte hain. Yeh pura Java mein likha gaya hai aur Java community mein bohot popular hai. JGit project Eclipse ke under aata hai, aur aapko yeh mil jaayega: https://www.eclipse.org/jgit/.

Getting Set Up
Aap apne project ko JGit se connect karne ke liye Maven use kar sakte ho. Aapko sirf apne pom.xml file mein yeh snippet add karna padega:
```
xml
Copy code
<dependency>
   <groupId>org.eclipse.jgit</groupId>
   <artifactId>org.eclipse.jgit</artifactId>
   <version>3.5.0.201409260305-r</version>
</dependency>
```
Version latest ho sakti hai, isliye check kar lena Maven repository par.

Agar aap binary dependencies khud manage karna chahte ho, toh pre-built JGit binaries yahan se download kar sakte ho. Fir aap command run karke apne project mein integrate kar sakte ho:
```
java -cp .:org.eclipse.jgit-3.5.0.201409260305-r.jar App
```
Plumbing
JGit do tarah ke APIs offer karta hai: plumbing aur porcelain. Plumbing APIs low-level repository objects ke saath interact karne ke liye hoti hain, jabki porcelain APIs user-level actions ke liye hoti hain, jo generally Git command line mein use hoti hain.

JGit mein zyada tar sessions ka starting point Repository class hota hai. Ek repository create karne ke liye:
```
// New repository create karo
Repository newlyCreatedRepo = FileRepositoryBuilder.create(new File("/tmp/new_repo/.git"));
newlyCreatedRepo.create();
```
Ek existing repository open karne ke liye:
```
Repository existingRepo = new FileRepositoryBuilder()
   .setGitDir(new File("my_repo/.git"))
   .build();
```
Aap Repository instance se bohot kuch kar sakte ho, jaise:

Reference lena:
```
Ref master = repo.getRef("master");
```
Object ko resolve karna:
```
ObjectId masterTip = master.getObjectId();
```
Branch create karna:
```
RefUpdate createBranch1 = repo.updateRef("refs/heads/branch1");
createBranch1.setNewObjectId(masterTip);
```
Branch delete karna:
```
RefUpdate deleteBranch1 = repo.updateRef("refs/heads/branch1");
deleteBranch1.setForceUpdate(true);
deleteBranch1.delete();
Config
```
Aap config se user ke naam jaise cheezein fetch kar sakte ho:
```
Config cfg = repo.getConfig();
String name = cfg.getString("user", null, "name");
```
JGit ke APIs kaafi wide hain aur bohot saari cheezein offer karti hain. Error handling ke liye JGit specific exceptions ka use karta hai jaise NoRemoteRepositoryException aur CorruptObjectException
# Go-Git
Go-Git ek pure Go library implementation hai, jo Git ko service mein integrate karne ke liye use hoti hai. Is implementation mein koi native dependencies nahi hain, isliye yeh manual memory management errors se bhi free hai. Yeh standard Golang performance analysis tools jaise CPU, memory profilers, race detector, etc. ke liye bhi transparent hai. 

Go-git extensibility, compatibility par focus karta hai aur ismein zyada tar plumbing APIs ko support kiya gaya hai, jo ki [documentation](https://github.com/go-git/go-git/blob/master/COMPATIBILITY.md) par available hai. Yahaan Go APIs ka ek basic example diya gaya hai:

```go
import "github.com/go-git/go-git/v5"

r, err := git.PlainClone("/tmp/foo", false, &git.CloneOptions{
   URL:      "https://github.com/go-git/go-git",
   Progress: os.Stdout,
})
``` 
