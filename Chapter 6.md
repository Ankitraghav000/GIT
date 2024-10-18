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

### Advanced Pull Requests

Ab jab humne GitHub pe project contribute karne ke basics samajh liye hain, to chaliye kuch interesting tips aur tricks ke baare mein baat karte hain taaki aap Pull Requests ko aur zyada effectively use kar paayein.

#### Pull Requests ko Patch ke Roop Mein Samajhna
Bahut important hai yeh samajhna ki kaafi saare projects Pull Requests ko ek aise tarike se nahi dekhte jaise mailing list-based projects patch series ko dekhte hain. Zyada tar GitHub projects Pull Requests ko ek iterative conversation ke roop mein dekhte hain jo final merge se pehle chalti hai.

Yeh ek important fark hai, kyunki Pull Requests mein code kabhi kabhi perfect nahi hota, jo mailing list-based patch series mein aksar hota hai. Pull Requests mein code propose kiya jaata hai jab wo perfect nahi hota, taaki maintainers aur community ke sath jaldi conversation ho sake. Agar maintainers ya community koi change suggest karein, to patch series ko re-roll nahi karte, balki naye commits add karte hain taaki purane ka context bana rahe.

Jaise, agar aap Pull Request dekhte hain to usme contributor ne rebase karke nayi Pull Request nahi bheji hoti. Balki naye commits add karke conversation ko aage badhaate hain. Jab aap site pe "Merge" button dabate hain, to ek merge commit banata hai jo original Pull Request se linked hota hai, taaki agar zarurat pade to pura conversation easily trace kiya ja sake.

##### Upstream Ke Sath Rehna
Agar aapki Pull Request outdated ho gayi ya conflict create kar rahi hai, to aapko ise fix karna hoga taaki maintainer asaani se ise merge kar sake. GitHub aapko bottom mein batayega agar koi merge conflict ho raha hai ya nahi.

Aapke paas do options hain: ya to aap apni branch ko rebase kar lein, ya target branch ko apni branch mein merge kar lein. Zyada tar developers dusra option choose karte hain, kyunki history aur final merge zyada important hota hai. Rebase karne se history clean hoti hai, lekin wo zyada mushkil aur error-prone bhi hota hai.

Agar aap merge karna chahte hain to ye steps follow karein:

Upstream repository ko remote add karein:
```
git remote add upstream https://github.com/schacon/blink
```
Latest work ko fetch karein:
```
git fetch upstream
```
Main branch ko apni branch mein merge karein:
```
git merge upstream/master
```
Agar conflicts hain to fix karein:
```
vim blink.ino
git add blink.ino
git commit
```
Changes ko push karein:
```
git push origin slow-blink
```
Iske baad, aapki Pull Request automatic update ho jaayegi aur phir se check ki jaayegi.

## Maintaining a Project
Agar aap GitHub pe ek project maintain karna chahte hain, toh aapko kai cheezein samajhni aur manage karni hongi, jaise nayi repository create karna, collaborators ko add karna, pull requests ko manage karna, etc. Yahaan har point ka detail me step-by-step explanation diya gaya hai.

### 1. Maintaining a Project
Ek project ko effectively maintain karne ke liye, aapko apne repository ka dhyan rakhna hota hai. Isme aapko ensure karna hota hai ki sabse latest changes properly update ho rahe hain, bugs fix ho rahe hain, aur naye features add ho rahe hain.
#### Steps:

- Regularly code ko update karna aur naye versions release karna.
- Issues track karna aur unka solution nikalna.
- Team ke sath collaboration karna aur contributors ke work ko review karna.
- Documentation aur guidelines ko update rakhna.
### 2. Nayi Repository Banana (Creating a New Repository)
Nayi repository banana GitHub pe kaam karne ka pehla step hota hai. Isme aapka project store hota hai jise duniya ke kisi bhi kone se access kiya ja sakta hai.
Steps:

- Dashboard pe “New Repository” button pe click kariye ya phir top me + button ke through "New repository" select kariye.
- Project name daliye, aur agar chahein toh description bhi de sakte hain.
- Public ya Private repository choose kariye.
- Agar chahein toh ek README.md file aur .gitignore file ko bhi initialize kar sakte hain.
- “Create Repository” button pe click kariye. Ab aapka project GitHub pe ready hai.
### 3. Collaborators Ko Add Karna (Adding Collaborators)
Agar aap dusre logon ko apne project me kaam karne dena chahte hain, toh aapko unhe collaborator bana kar repository ka access dena hoga.
Steps:

- Apni repository ke page pe jaake “Settings” option choose kariye.
- Left-hand side me “Collaborators” option pe click kariye.
- Username ya email id dalke “Add collaborator” pe click kariye.
- Jise aap add karenge, usse ek invite milega, aur wo accept karne ke baad repository pe push kar sakega.
### 4. Pull Requests Manage Karna (Managing Pull Requests)
Jab koi contributor project me koi change karta hai, toh wo changes ko merge karwane ke liye pull request (PR) bhejta hai. PR ko review karna aur merge karna ek important task hota hai.
Steps:

Jab koi PR create hota hai, aapko ek notification milta hai.
Aap PR ka diff (changes) check kar sakte hain, files ko compare kar sakte hain, aur comments add kar sakte hain.
Agar sab kuch sahi ho, toh PR ko “Merge” kar dijiye, ya fir aapko lagta hai kuch changes chahiye, toh "Request Changes" option use kariye.
### 5. Pull Request Pe Collaboration (Collaborating on the Pull Request)
Pull request pe aap aur contributor milkar changes pe discussion kar sakte hain. Yeh ek tarike ka code review process hota hai.
Steps:

PR me comments section ka use karke aap suggestions de sakte hain.
Aap ek commit push kar sakte hain ya contributor se changes karne ka request kar sakte hain.
Pull request ko tab tak open rakha ja sakta hai jab tak sab changes finalize nahi ho jaate.
### 6. Pull Request Pe Pull Request (Pull Requests on Pull Requests)
Kabhi-kabhi ek PR pe naye changes karne ke liye dusra PR bhi banaya ja sakta hai. Is tarah ke workflows bade projects me use hote hain.
Steps:

Kisi aur contributor ka PR accept hone se pehle uske code me naye changes lane ke liye ek alag branch bana sakte hain.
Us branch ka PR original PR ke sath link kiya ja sakta hai.
Isse multiple layers of review aur changes handle karne me madad milti hai.
### 7. Mentions Aur Notifications (Mentions and Notifications)
GitHub me aap kisi user ko mention kar sakte hain (@username) jisse unhe uske baare me notification milti hai. Yeh process collaboration aur fast response ke liye kaafi helpful hota hai.
Steps:

Issue ya PR me @username likhkar kisi ko mention kariye.
Mentioned user ko us notification ke zariye us PR ya Issue ke baare me turant pata chal jayega.
### 8. Notifications Page (The Notifications Page)
GitHub ka notification page ek centralized jagah hoti hai jaha aapko sabhi projects ke updates dikhte hain jisme aap involved hain.
Steps:

GitHub ke top-right corner me bell icon pe click karke aap notifications dekh sakte hain.
Yaha se aap notifications ko read, archive ya ignore kar sakte hain.
### 9. Web Notifications aur Email Notifications
Notifications ko aap directly GitHub pe ya apne email ke zariye bhi paa sakte hain.
Web Notifications:

Browser ke notifications aapko turant batate hain jab koi important change ya mention hoti hai.
Email Notifications:
Aap apne email pe notifications ko receive karne ke liye GitHub ki settings se configure kar sakte hain.
### 10. Special Files (README, CONTRIBUTING)
Kuch files aapke project ko maintain karne me madad karti hain aur contributors ko guide karti hain.

README.md: Yeh file project ka introduction hoti hai, jisme aap installation steps, usage instructions aur features batate hain.

Example:

markdown
```
# Project Name
Project description.

## Installation
How to install the project.

## Usage
Instructions to use the project.
```
### CONTRIBUTING.md:
Yeh file contributors ko batati hai ki project me kaise contribute karein, kya guidelines follow karni hain, aur kaise PRs banayein.
Managing an Organization
GitHub par sirf single-user accounts ke ilawa "Organizations" bhi hoti hain. Jaise personal accounts ka namespace hota hai jahan unke saare projects store hote hain, waise hi organization ke accounts ka bhi ek namespace hota hai. Lekin, kaafi cheezen alag hoti hain. Yeh accounts un logon ke group ko represent karte hain jo projects ka shared ownership rakhte hain, aur kaafi tools diye gaye hain jo logon ke subgroups ko manage karte hain. Normally, yeh accounts open source groups (jaise "perl" ya "rails") ya companies (jaise "google" ya "twitter") ke liye use hote hain.

## Organization Basics
Organization banana kaafi aasaan hai. Aapko GitHub ke kisi bhi page ke top-right corner mein "plus" icon pe click karna hoga, aur menu se "New organization" select karna hoga.

Sabse pehle, aapko apne organization ka naam dena hoga aur ek email address provide karna hoga jo group ke liye main point of contact hoga. Aap chaho toh doosre users ko co-owners bana sakte ho. Yeh steps follow karo aur jaldi hi aapke paas ek nayi organization ka ownership aa jayega. Jaise personal accounts, waise organizations bhi tab tak free hain jab tak aap jo bhi data store kar rahe ho wo open source rahega.

Owner hone ke naate, jab aap koi repository fork karte ho, toh aapke paas apni organization ke namespace mein fork karne ka option hoga. Jab aap naye repositories banate ho, toh aap apne personal account ya kisi bhi organization ke naam pe jo aap own karte ho, create kar sakte ho. Aap automatically "watch" karte ho koi bhi nayi repository jo organization ke under create ki gayi ho.

Jaise personal accounts mein aap apna avatar upload karte ho, waise organization ke liye bhi aap avatar upload kar sakte ho takki usko personalize kiya ja sake. Aur, jaise personal accounts ke liye landing page hota hai, waise hi organization ka bhi landing page hota hai jisme saare repositories list hote hain jo doosre log dekh sakte hain.

Ab hum kuch differences dekhte hain jo organization account ke sath aate hain.

### Teams
Organizations individual logon ko teams ke zariye associate karti hain, jo ki basically individual user accounts aur repositories ka grouping hota hai, aur ye bhi define karta hai ki un logon ko kaunsa access milta hai.

Misal ke taur par, maan lo aapki company ke paas teen repositories hain: frontend, backend, aur deployscripts. Aap apne HTML/CSS/JavaScript developers ko frontend aur shayad backend ka access dena chahenge, aur Operations logon ko backend aur deployscripts ka access milega. Teams ke zariye aapko har repository ke liye individual collaborators manage karne ki zaroorat nahi hoti.

Organization page aapko ek simple dashboard dikhata hai jisme organization ke under aane wale saare repositories, users, aur teams ka view hota hai.

Teams ko manage karne ke liye, aap "Teams" sidebar pe click kar sakte ho jo Organization page ke right-hand side mein hota hai. Yeh aapko ek page pe le jata hai jaha aap team mein members add kar sakte ho, repositories add kar sakte ho, ya team ki settings aur access control levels ko manage kar sakte ho. Har team ko read-only, read/write, ya administrative access milta hai repositories pe. Yeh level aap "Settings" button click karke change kar sakte ho jo Team page mein hota hai.

Jab aap kisi ko team mein invite karte ho, toh unko ek email milta hai jisme bataya jata hai ki unko invite kiya gaya hai.

Team @mentions (jaise @acmecorp/frontend) waise hi kaam karte hain jaise individual users ke saath hota hai, bas farq yeh hai ki team ke sabhi members us thread ko subscribe kar lete hain. Yeh tab useful hota hai jab aapko kisi team member se help chahiye, lekin aapko exact nahi pata hota kis se puchhna hai.

Ek user kisi bhi number of teams mein ho sakta hai, toh sirf access-control teams tak limit mat rakhna. Special-interest teams jaise ux, css, ya refactoring specific questions ke liye useful hote hain, aur doosre teams jaise legal aur colorblind alag tarah ke kaamon ke liye helpful hote hain.

### Audit Log
Organizations ke owners ko organization ke andar hone wali saari activities ka access milta hai. Aap 'Audit Log' tab pe jaake dekh sakte ho ki organization level pe kya events hue, kisne kiye aur kaha se kiye gaye.

Aap specific types of events, specific jagah ya specific logon ke hisaab se filter bhi kar sakte ho.
## GitHub Scripting
Ab humne GitHub ke major features aur workflows cover kar liye hain, lekin agar koi bada project ya group ho toh unke paas apni customizations hoti hain ya phir woh external services integrate karna chahte hain.

Khus kismati se, GitHub kaafi hackable hai. Iss section mein hum dekhenge kaise GitHub hooks system aur API ko use karke GitHub ko apne hisaab se customize kar sakte hain.

#### Services aur Hooks
GitHub ke Hooks aur Services section mein aap easily external services ko integrate kar sakte ho. Yeh options aapko repository settings mein milte hain, jahan hum pehle collaborators add karne aur default branch change karne ke options dekh rahe the. Aapko "Webhooks aur Services" tab mein Services aur Hooks configuration milega.

#####  Services
Pehle hum Services ko dekhenge. Yeh wo integrations hain jo GitHub ko doosri systems, jaise Continuous Integration services, bug/issue trackers, chat rooms, documentation systems, waqera ke sath connect karte hain. Example ke liye, agar aap Jenkins ko use kar rahe ho apni codebase ka test chalane ke liye, toh Jenkins ka builtin service enable kar sakte ho, taaki jab koi push kare, toh Jenkins automatic test run kare.

Hum ek simple service setup karenge - Email hook. Agar aap "email" select karte ho "Add Service" dropdown se, toh ek configuration screen open hogi:

Example:

Email address enter karo, aur jab koi push karega, toh specified email address par notification aayega.
Yeh services alag-alag events par listen kar sakti hain, but mostly yeh push events par kaam karti hain.

### Hooks
Agar aapko koi aur specific customization chahiye ya koi service list mein nahi hai, toh aap generic Hooks system ka use kar sakte ho. Hooks allow karte hain ke jab bhi koi event (jaise push, issue open, waqera) ho, toh GitHub ek HTTP payload bheje aapke defined URL par.

Aapko bas ek URL specify karna hota hai, aur GitHub us URL par payload send kar deta hai jab bhi specified event hota hai. Example ke liye, agar aap chahte ho ke jab koi specific branch par push kare, aur ek specific file modify ho, toh aap webhook configure kar sakte ho.

Example Webhook:
```
require 'sinatra'  
require 'json'  
require 'mail'

post '/payload' do  
  push = JSON.parse(request.body.read) # Payload JSON parse karte hain  
  pusher = push["pusher"]["name"]  
  branch = push["ref"]
  
  files = push["commits"].map do |commit|  
    commit['added'] + commit['modified'] + commit['removed']  
  end  
  
  files = files.flatten.uniq
  
  # Agar specific file aur branch par push hoti hai toh email bhejte hain  
  if pusher == 'schacon' &&   branch == 'refs/heads/special-branch' &&   files.include?('special-file.txt')  
    Mail.deliver do  
      from 'tchacon@example.com'  
      to 'tchacon@example.com'  
      subject 'Scott Changed the File'  
      body 'ALARM'  
    end  
  end  
end
```
Is code mein hum payload parse karte hain, pusher ka name, branch, aur files check karte hain. Agar criteria match hoti hai, toh ek email bhejte hain.

GitHub ke hook debugging tools se aap yeh dekh sakte ho ke last payload kahan deliver hua, successful tha ya nahi, waqera.

### GitHub API
Services aur hooks allow karte hain push notifications receive karna jab koi event hota hai. Lekin agar aapko aur zyada information chahiye ya kuch automate karna hai jaise collaborators add karna ya issues label karna, toh GitHub API ka use kar sakte hain.

API ke through aap koi bhi kaam automate kar sakte ho jo aap GitHub website par manually karte ho.

- Basic Example
Sabse basic kaam jo aap kar sakte ho wo hai ek simple GET request jo authentication nahi maangta. Example ke liye, agar hum ek user "schacon" ke baare mein jaana chahte hain:

bash
```
$ curl https://api.github.com/users/schacon

{
  "login": "schacon",
  "id": 70,
  "avatar_url": "https://avatars.githubusercontent.com/u/70",
  "name": "Scott Chacon",
  "company": "GitHub",
  "following": 19,
  "created_at": "2008-01-27T17:19:28Z",
  "updated_at": "2014-06-10T02:37:23Z"
}
```
Aap iss tarah se bahut saari information le sakte ho jaise issues, commits, organizations, waqera ke baare mein.


#### Pull Request Status Change Karna
Ek aur useful feature hai Pull Request status change karna. Yeh feature Continuous Integration services use karti hain jab code test hota hai aur wo status report karti hain (pass/fail). Aap isse aur bhi checks ke liye use kar sakte ho jaise sign-off check, commit message formatting waqera.

```
require 'httparty'  
require 'sinatra'  
require 'json'

post '/payload' do  
  push = JSON.parse(request.body.read) # Payload parse karte hain  
  repo_name = push['repository']['full_name']

  push["commits"].each do |commit|  
    if /Signed-off-by/.match commit['message']  
      state = 'success'  
      description = 'Successfully signed off!'  
    else  
      state = 'failure'  
      description = 'No signoff found.'  
    end

    sha = commit["id"]  
    status_url = "https://api.github.com/repos/#{repo_name}/statuses/#{sha}"

    status = {  
      "state"       => state,  
      "description" => description,  
      "target_url"  => "http://example.com/how-to-signoff",  
      "context"     => "validate/signoff"  
    }  

    HTTParty.post(status_url,  
      :body => status.to_json,  
      :headers => {  
        'Content-Type'  => 'application/json',  
        'User-Agent'    => 'tonychacon/signoff',  
        'Authorization' => "token #{ENV['TOKEN']}" }  
    )  
  end  
end
```
Yahan par webhook handler checks karta hai commit messages mein 'Signed-off-by' string ke liye. Agar message match hota hai toh success status post karte hain, warna failure.
### Octokit
Octokit ek simple tool hai jo GitHub ke saath kaam karne ke liye use hota hai. Isse aap GitHub pe apne repositories, issues, aur pull requests ko manage kar sakte ho bina complex coding kiye.

Example:
Agar aapko apna GitHub account se data nikalna hai, jaise apna username, toh aap Octokit se asaani se kar sakte ho.

JavaScript ka simple example:
```
const { Octokit } = require("@octokit/rest");  // Octokit ko import kar rahe hain

const octokit = new Octokit({
  auth: 'aapka-github-token'  // Apna GitHub token yaha daalein
});

octokit.rest.users.getAuthenticated()
  .then(({ data }) => {
    console.log(data.login);  // Aapka GitHub username dikhayega
  });
```
Is example mein hum GitHub se apna username nikal rahe hain, aur Octokit is process ko kaafi simple bana deta hai. Aapko bas token daalna hota hai aur Octokit baaki ka kaam khud kar leta hai.







