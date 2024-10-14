# Distributed Git
Ab jab aapne remote Git repository setup kar liya hai jise sabhi developers apne code share karne ke liye istemal karte hain, aur aap local workflow mein basic Git commands ke saath parichit hain, aap dekhenge ki Git ke distributed workflows kaise kaam karte hain.

Is chapter mein, aap Git ko distributed environment mein ek contributor aur integrator ke roop mein kaise istemal karein, yeh seekhenge. Aap seekhenge ki ek project mein code kaise successfully contribute karein aur project maintainer ke liye ise asan bana dein, aur kaise ek project ko kai developers ke saath milkar successfully maintain karein.

## Distributed Workflow in Git
Git ke distributed workflow se developers ko projects par kaam karne ki zyada flexibility milti hai. Isme har developer apne local repository ka istemal karke code bana sakta hai aur dusre developers ke saath asaani se share kar sakta hai. Yahan kuch common distributed workflows hain:

### Centralized Workflow
Centralized systems mein, ek hi collaboration model hota hai — centralized workflow. Ek central hub ya repository code accept karta hai, aur sab log apne kaam ko uske sath synchronize karte hain.

Workflow:

Multiple developers hub se clone karte hain.
Pehla developer apne changes push karta hai.
Dusra developer apne changes push karne ki koshish karta hai, lekin server unhe reject kar deta hai. Unhe pehle changes fetch aur merge karne hote hain.
Is workflow ko bahut log pasand karte hain kyunki yeh unke liye familiar aur comfortable hai.
