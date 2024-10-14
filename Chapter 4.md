# Git on the Server
Ab tak aap Git ke day-to-day tasks karne ke liye tayaar hain, lekin collaboration karne ke liye aapko ek remote Git repository ki zaroorat hai. Aap technically kisi bhi individual ke repositories mein changes push aur pull kar sakte hain, lekin aisa karna discouraged hai, kyunki agar aap dhyan nahi rakhte toh aap aasani se confuse ho sakte hain ki doosre log kya kar rahe hain.

Iske alawa, aap chahte hain ki aapke collaborators repository ko access kar sakein, chahe aapka computer offline hi kyun na ho. Isliye, ek intermediate repository set up karna behtar hota hai, jisse aap dono access kar sakein aur us par push aur pull kar sakein.

## Git Server Chalayana
Git server chalana kaafi straightforward hai. Sabse pehle, aapko yeh decide karna hoga ki aapka server kaunse protocols support karega. Is chapter ke pehle section mein available protocols ke pros aur cons cover kiye jayenge. Agle sections mein, in protocols ka use karke typical setups aur server ko chalane ka tarika bataya jaayega.

Agar aap apna khud ka server chalane mein interested nahi hain, toh aap chapter ke aakhri section par skip kar sakte hain jahan hosted account set up karne ke options diye gaye hain, aur phir agle chapter mein move kar sakte hain, jahan distributed source control environment ke various aspects discuss kiye jayenge.

##   Remote Repository Kya Hota Hai?
Ek remote repository aam taur par ek bare repository hoti hai — ek Git repository jisme koi working directory nahi hoti. Kyunki repository ka use sirf collaboration point ke liye hota hai, isliye disk par checked-out snapshot hone ki koi zaroorat nahi hai; yeh sirf Git data hota hai.

Bare Repository ka matlab hai aapke project ki .git directory ka content aur kuch nahi. Is tarike se, aapka project clean aur organized rahta hai, aur aap asani se doosre collaborators ke saath kaam kar sakte hain.

Git mein protocols ka istemal data transfer ke liye hota hai. Yeh protocols define karte hain ki Git repository ke sath kaise communicate kiya jaye. Git ke chaar mukhya protocols hain: Local, HTTP, SSH, aur Git. In sabhi protocols ka istemal alag situations mein kiya ja sakta hai.
## protocols
Yahan, in protocols ko samjhaate hain aur saath hi unke commands bhi dete hain:

1. Local Protocol
Local protocol tab istemal hota hai jab aapka remote repository same machine par ho. Yeh sabse aasaan aur fastest method hai.

Command:
```
git clone /path/to/local/repository.git
```
Example:

```
git clone /srv/git/myproject.git
```
2. HTTP Protocols
HTTP protocols do types ke hote hain: Smart HTTP aur Dumb HTTP.

a. Smart HTTP Ismein aap Git ko HTTP ke through communicate karne ke liye keh sakte hain. Yeh authentication aur push/pull operations ko support karta hai.

Command:
```
git clone http://example.com/repository.git
```
Example:
```
git clone http://mywebsite.com/myproject.git
```
b. Dumb HTTP Ismein server ko normal files ki tarah serve kiya jata hai, bina kisi authentication ke. Yeh basic HTTP request ko support karta hai.

Command:
```
git clone http://example.com/myproject.git
```
Yeh command use karne par aapko bare Git repository ko HTTP ke zariye access karne ko milega.

3. SSH Protocol
SSH (Secure Shell) protocol secure data transfer ke liye istemal hota hai. Ismein aapko authentication ke liye username aur password ka istemal karna hota hai.

Command:
```
git clone ssh://username@host:/path/to/repository.git
```
Example:
```
git clone ssh://user@myserver.com/myproject.git
```
Ya aap is short form ka bhi istemal kar sakte hain:
```
git clone user@myserver.com:myproject.git
```
4. Git Protocol
Git protocol ek special daemon hai jo Git ke sath bundled hota hai. Yeh fast hai aur port 9418 par sunta hai. Ismein koi authentication nahi hoti.

Command:
```
git clone git://host/repository.git
```
Example:
```
git clone git://mygitserver.com/myproject.git
```
## Getting Git on a Server
Git server set up karne ke liye, aapko apne server par Git service install karni hoti hai. Hum yahan Linux-based server par basic installation ke commands aur steps cover karenge. MacOS ya Windows servers par bhi ye services chalana mumkin hai, lekin production server setup karte waqt aapko security measures aur operating system tools mein kuch differences dekhne ko mil sakte hain.

Git Server Setup Karna
Bare Repository Banana: Kisi bhi Git server ko pehle set up karne ke liye, aapko ek existing repository ko new bare repository mein export karna hota hai. Bare repository aisa repository hota hai jisme working directory nahi hoti. Ye kaafi simple hai.

Command:
```
git clone --bare my_project my_project.git
```
Example:
```
Cloning into bare repository 'my_project.git'... done.
```
Yeh command my_project.git directory mein Git directory data ka copy banayega. Iska matlab yeh hai ki aap:
```
cp -Rf my_project/.git my_project.git
```
yeh command bhi use kar sakte hain.

Bare Repository Server Par Rakhna: Ab aapke paas ek bare copy hai, toh isay server par rakhna hoga. Agar aapne git.example.com server set up kiya hai jahan aapko SSH access hai, toh aap apne bare repository ko /srv/git directory mein store kar sakte hain.

Command:
```
scp -r my_project.git user@git.example.com:/srv/git
```
Ab, agar kisi aur user ke paas /srv/git directory par SSH-based read access hai, toh woh aapki repository ko clone kar sakta hai:

```
git clone user@git.example.com:/srv/git/my_project.git
```
Agar user server par SSH karta hai aur usay /srv/git/my_project.git directory par write access hai, toh usay push access bhi milega.

Shared Repository Setup: Git automatically group write permissions ko add kar deta hai agar aap git init command ko --shared option ke sath run karte hain.

Command:
```
ssh user@git.example.com
cd /srv/git/my_project.git
git init --bare --shared
```
Yeh kaam aasan hai! Aapne ek Git repository le li, bare version banaya, aur server par rakh diya, jahan aap aur aapke collaborators SSH access rakhte hain.
## SSH Public Key Generate Karna
Bohot saare Git servers SSH public keys ka use karte hain authenticate karne ke liye. Har user ko apna public key generate karna hota hai agar unke paas pehle se nahi ho. Yeh process lagbhag har operating system mein similar hota hai.

Check karna agar key pehle se hai: By default, SSH keys .ssh directory mein hoti hain. Aap is command se check kar sakte ho:

```
$ cd ~/.ssh
$ ls
```
Agar id_rsa ya id_dsa jaisa kuch file dikh raha ho aur .pub extension wala file bhi ho, toh public key hai.

Agar key nahi hai, toh generate karne ke liye:
```
$ ssh-keygen -o
```
Isse ek public-private key pair generate hota hai. Aapko passphrase bhi dalna hota hai, par agar aap chaho toh blank chod sakte ho.

Public Key ko Copy Karna: Apne public key ko copy karke kisi bhi admin ya server ko bhejna hota hai, jo Git server manage kar raha ho. Yeh key kuch aise dikhti hai:
```
$ cat ~/.ssh/id_rsa.pub
```
Server Setup Karna :

SSH access ko server side par set up karne ke liye pehle ek git user account banana padta hai aur ek .ssh directory create karni hoti hai.
```
$ sudo adduser git
$ su git
$ mkdir .ssh && chmod 700 .ssh
$ touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
```
Ab authorized_keys file mein developers ke public keys ko add karna hoga:
```
$ cat /tmp/id_rsa.john.pub >> ~/.ssh/authorized_keys
```
## Git Daemon
Git Daemon ek lightweight server process hai jo Git protocol ke zariye repositories ko serve karta hai. Ye server specifically read-only access ke liye hota hai, aur ye unauthenticated hota hai, matlab jo bhi repositories aap isse serve karte ho, unko koi bhi bina authentication ke access kar sakta hai (jaise SSH key ya username/password ke bina).

Ye setup commonly aise projects ke liye use hota hai jo public hai ya jo aapko large number of people ke liye accessible banana hai, bina har ek ke liye credentials manage kiye.
## Smart HTTP
Smart HTTP ek Git protocol hai jo dono authenticated aur unauthenticated access provide karta hai ek hi time pe. Matlab, aap isko use karke SSH jaise authentication aur git:// jaise fast, unauthenticated access dono le sakte ho. Yeh setup Git's smart HTTP backend ke zariye hota hai.
## GitWeb
GitWeb ek web-based visualizer hai jo aapke Git repositories ko simple interface mein dikhata hai. Agar aap chaahte ho ki aapke project ke read/write access ke saath ek web interface bhi ho, toh aap GitWeb setup kar sakte ho. Isse aap apne Git projects ko browser mein dekh paoge.

GitWeb Setup Kaise Karein?
Step 1: Temporary Setup using Git Instaweb

Agar aap sirf temporary basis par apne project ka GitWeb UI dekhna chahte ho, toh aap git instaweb command use kar sakte ho.

Agar aapke system mein ek lightweight web server jaise lighttpd installed hai, toh aap easily temporary server chala sakte ho:
```
$ git instaweb
```
Agar aap macOS use kar rahe ho toh aap Ruby ke saath preinstalled webrick web server use kar sakte ho:

```
$ git instaweb --httpd=webrick
```
Yeh command ek HTTP server start karega (default port 1234 pe) aur automatically aapka browser open kar dega jisme aap apne project ko dekh sakte ho.

Server ko stop karne ke liye:

```
$ git instaweb --httpd=webrick --stop
```
## GitLab
GitLab ek powerful tool hai jo Git repositories ke liye web interface provide karta hai. Iska istemal projects ko manage karne, collaboration karne, aur source code ko version control karne ke liye hota hai. Yahan par kuch important features aur concepts hain jo GitLab mein hain:

Groups
Groups GitLab mein users ka ek collection hota hai. Har group ke saath kuch users associated hote hain, jinka permission level alag hota hai. Permission levels "Guest" se lekar "Owner" tak hote hain. "Owner" ko group aur uske projects ka full control hota hai.
Projects
Projects GitLab mein ek Git repository ke roop mein hota hai. Har project ek namespace se associated hota hai, ya to user ka ya group ka. Agar project kisi user ke paas hai, toh us user ka control hota hai ki kis kis ko access milega.

Visibility Levels: Har project ki visibility level hoti hai:

Private: Sirf specific users ko access diya jata hai.
Internal: Kisi bhi logged-in user ko visible hota hai.
Public: Sabhi ko visible hota hai.
## Basic Usage
New Project Create Karna: GitLab mein naya project create karne ke liye toolbar par "+" icon par click karein. Yahan aapko project ka naam, namespace, aur visibility level specify karna hoga. Phir "Create Project" par click karein.

Local Git Repository se Connect Karna:

Existing local repository ke liye:
```
git remote add gitlab https://server/namespace/project.git
```
Naya repository clone karne ke liye:
```
git clone https://server/namespace/project.git
```
