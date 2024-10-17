# GitHub 
GitHub ek web-based platform hai jo Git version control system ko use karke projects ko host karta hai. Is platform ka use developers aur teams open-source aur private projects pe collaborate karne ke liye karte hain. GitHub ko primarily Git repositories ke liye use kiya jaata hai, jisme aap apne source code ko store, manage, aur version control kar sakte ho.

GitHub mainly open-source projects ke liye popular hai, lekin private repositories ke liye bhi iska use hota hai.

## GitHub Account Setup and Configuration 
### Step 1: Sign Up on GitHub
Sabse pehle aapko GitHub pe ek account banana hoga. Iske liye:
- Visit Website: Browser me https://github.com khol lo.
- Sign Up: Top-right corner pe green button "Sign up for GitHub" pe click karo.
- Username, Email, Password: Apna unique username, email address, aur password enter karo.
Verification: GitHub aapko ek verification email bhejega. Us email ko open karke account verify karo.
### Step 2: Basic Profile Setup
Account banne ke baad, aapko apne profile ko setup karna hoga:
- Upload Avatar: Aap apni profile picture ya avatar set kar sakte ho.
- Add Bio: Apne profile me ek chhoti bio likho, taaki dusre users ko aapke baare me pata chale.
- Location: Apna location add kar sakte ho.
### Contributing to a Project
Ab jab humara GitHub account setup ho gaya hai, toh chaliye dekhte hain kaise aap kisi existing project mein contribute kar sakte hain.

#### Forking Projects
Agar aap kisi aise project mein contribute karna chahte hain jisme aapko push karne ka access nahi hai, toh aap project ko “fork” kar sakte hain. Jab aap “fork” karte hain, GitHub us project ki ek copy bana deta hai jo aapki apni hoti hai, aur aap uspe push kar sakte hain.

Fork ka purana matlab kuch alag hota tha, jisme koi open source project ko ek nayi direction mein le jaata tha, kabhi-kabhi competition create karke contributors ko split karta tha. Lekin GitHub mein “fork” sirf ek simple project ki copy hoti hai jo aapke namespace mein hoti hai. Isse aap publically project ko modify kar sakte hain, jo aapki contribution ko open tariqe se dikhata hai.

Fork karne ke baad, aapko collaborators add karne ki zarurat nahi hoti. Log project ko fork karte hain, usme changes karte hain, aur phir “Pull Request” ke through changes wapas original project mein contribute karte hain.

Fork karne ke liye: Project page par jaaiye aur upar-right corner mein "Fork" button par click kariye.

#### GitHub Flow
GitHub ek collaboration workflow par design kiya gaya hai jo mainly “Pull Requests” par center hota hai. Yeh flow tab bhi kaam karta hai jab aap ek chhoti team ke saath ya globally distributed company ke saath kaam kar rahe hote hain. Yahan ek high-level overview diya gaya hai:

1. Project ko Fork kariye.
2. Master branch se ek nayi topic branch banaiye.
3. Project mein kuch commits kariye taaki improvement ho sake.
4. Is branch ko aapke GitHub project par push kariye.
5.GitHub par ek Pull Request banaiye.
6. Discuss kariye, aur zarurat padne par further commits kariye.
7. Project owner aapki Pull Request ko merge ya close karega.
8. Sync karke updated master wapas aapke fork mein le aaiye.
Example: Pull Request Banana
Maan lijiye Tony Arduino ke liye code dhoondh rahe hain aur unhe ek achha program file GitHub par milta hai. Lekin blinking rate thoda fast hai, toh hum is program ko thoda modify karke owner ko suggest karenge.

Steps:

Project ko fork karke apni copy banaiye.
Apni copy ko clone kariye.
```
git clone https://github.com/tonychacon/blink
```
Ek nayi topic branch banaiye:
```
git checkout -b slow-blink
```
Apne code mein changes kariye (yahan blink speed ko modify kar rahe hain):
```
sed -i '' 's/1000/3000/' blink.ino  # macOS
sed -i 's/1000/3000/' blink.ino  # Linux
```
Changes ko commit kariye:
```
git commit -a -m 'Change delay to 3 seconds'
```
Branch ko GitHub par push kariye:
```
git push origin slow-blink
```
Pull Request Banana
Ab GitHub aapke project ko detect karega aur aapko ek option dega "Pull Request" banane ka. Aapko ek title aur description dalna hoga jo project owner ko aapke changes samajhne mein madad karega.

Iterating on Pull Requests
Jab project owner aapke Pull Request ko review karega, wo ya toh changes ko merge karega, ya reject karega, ya kuch comments suggest karega. Aap un comments ke hisaab se apni branch mein further commits kar sakte hain.

Jab aap commits push karenge, Pull Request automatically update ho jaata hai.

Is tarah aap GitHub par kisi bhi public ya internal project mein contribute kar sakte hain.
