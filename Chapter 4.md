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
