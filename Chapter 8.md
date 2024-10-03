# Git Configuration
Git configuration settings ko aap git config command se customize kar sakte ho, jaisa ki aapne shuruaat mein apna name aur email address set kiya tha:
```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```
Client Configuration
Git mein configuration options do categories mein aati hain: client-side aur server-side. Zyada options client-side hote hain jo aapki personal working preferences ko set karte hain. Bohot saare configuration options supported hote hain, lekin kuch sirf specific scenarios ke liye useful hote hain. Agar aapko apni Git version ke sare options dekhne hain, to yeh command run karo:
```
$ man git-config
```
core.editor
By default, Git jo bhi aapka shell editor hai, wo use karta hai (like vi, nano, etc.). Agar aap kuch aur use karna chahte ho, to yeh command run karo:
```
$ git config --global core.editor emacs
```
Iske baad, har baar commit message edit karne ke liye emacs open hoga.
## commit.template
Agar aap chahte ho ki har commit ke liye ek default message aaye, to ek custom template file set kar sakte ho. Jaise, yeh template create karo:
```
$ nano ~/.gitmessage.txt
```
Aur usmein yeh likho:
```
Subject line (50 characters ke andar rakhne ki koshish karo)
Detailed description of commit.
[Ticket: X]
```
Ab, yeh file use karne ke liye:
```
$ git config --global commit.template ~/.gitmessage.txt
```
Iske baad jab bhi git commit command doge, yeh template default message ke roop mein dikhai dega.
## core.pager
Yeh setting decide karti hai ki Git ka output kis tool ke through paginate hoga, default mein less hota hai. Agar aapko pagination nahi chahiye, to ise blank set kar sakte ho:
```
$ git config --global core.pager ''
```
Isse jitna bhi output hoga, wo direct terminal pe dikhai dega, bina pause ke.

## user.signingkey
Agar aap commits ya tags sign kar rahe ho, to apna GPG signing key set karne ke liye:
```
$ git config --global user.signingkey <gpg-key-id>
```
Iske baad har baar key specify karne ki zarurat nahi padegi.
## core.excludesfile
Agar aapko globally kuch files ko ignore karna hai (e.g. .DS_Store ya *~), to aap .gitignore_global file create karke usmein add kar sakte ho. Jaise:
```
$ nano ~/.gitignore_global
```
Usmein likho:
```
markdown
Copy code
*~  
.*.swp  
.DS_Store
```
Aur fir Git ko batao ki yeh global ignore list use kare:
```
$ git config --global core.excludesfile ~/.gitignore_global
```
## help.autocorrect
Agar aap galti se koi command wrong type karte ho, to Git us command ko autocorrect kar sakta hai. Example:
```
$ git config --global help.autocorrect 1
```
Ab agar aap galat command likhoge jaise git chekcout, to Git ise automatically correct karke run karega.

## color.ui
Git ke output ko colorize karne ke liye:
```
$ git config --global color.ui auto
```
Ya agar aap color nahi chahte, to ise off karne ke liye:
```
$ git config --global color.ui false
```
## External Merge and Diff Tools
Git ke internal implementation ke alawa, aap external tools set up kar sakte hain jise aap diff aur merge conflicts resolve karne ke liye use kar sakte hain. Hum yahan Perforce Visual Merge Tool (P4Merge) ka istemal karenge, kyunki ye ek achha graphical tool hai aur free bhi hai.

P4Merge Set Up Karna:
Download Karo P4Merge:

Wrapper Scripts Set Up Karo:
Ek merge wrapper script banayein extMerge naam se:
```
cat /usr/local/bin/extMerge
#!/bin/sh
/Applications/p4merge.app/Contents/MacOS/p4merge $*
```
Ek diff wrapper script banayein extDiff naam se:
```
cat /usr/local/bin/extDiff
#!/bin/sh
[ $# -eq 7 ] && /usr/local/bin/extMerge "$2" "$5"
```
Scripts ko Executable Banao:
```
sudo chmod +x /usr/local/bin/extMerge
sudo chmod +x /usr/local/bin/extDiff
```
Config File Set Up Karo: Apne config file ko customize karne ke liye ye commands run karo:
```
git config --global merge.tool extMerge
git config --global mergetool.extMerge.cmd 'extMerge "$BASE" "$LOCAL" "$REMOTE" "$MERGED"'
git config --global mergetool.extMerge.trustExitCode false
git config --global diff.external extDiff
```
Diff Command Chalayen:
```
git diff 32d1776b1^ 32d1776b1
```
Ye command P4Merge ko launch karega.

Merge Conflicts Resolve Karna: Agar aap merge karte hain aur conflicts aate hain, to command run karein:
```
git mergetool
```
## Whitespace aur Formatting Issues
Formatting aur whitespace issues cross-platform development mein common hain. Isko handle karne ke liye Git kuch configuration options offer karta hai.

Line Endings ko Handle Karna:

Agar aap Windows pe hain, to is command se core.autocrlf ko true karein:
```
git config --global core.autocrlf true
```
Agar aap macOS ya Linux pe hain, to isko input par set karein:
```
git config --global core.autocrlf input
```
Windows-only projects ke liye, false par set karein:
```
git config --global core.autocrlf false
```
Whitespace Issues Ko Detect Karna:

Git kuch whitespace issues ko detect karta hai. Aapko set karna hoga ki kaun se issues check hone chahiye:
```
git config --global core.whitespace trailing-space,-space-before-tab,indent-with-non-tab,tab-in-indent,cr-at-eol
```
Patch apply karte waqt whitespace issues ke liye warning dekhna:
```
git apply --whitespace=warn <patch>
```
Automatically fix karna:
```
git apply --whitespace=fix <patch>
```
Agar aapne commit kar diya aur push nahi kiya, to whitespace issues ko fix karne ke liye:
```
git rebase --whitespace=fix
```
# Server Configuration in Git
Git ke server side ke liye kuch khaas configuration options hote hain jo aapko dhyan me rakhne chahiye. In options ka istemal karke aap apne repository ko behtar tarike se manage kar sakte hain. Yahan kuch mahatvapurn settings di gayi hain:

1. receive.fsckObjects
Yeh option ensure karta hai ki jab bhi koi push hoti hai, toh usmein jo bhi objects hain, unka SHA-1 checksum sahi hai ya nahi. Yeh by default nahi hota, lekin aap isko enable kar sakte hain:
```
$ git config --system receive.fsckObjects true
```
Isse Git har push se pehle repository ki integrity check karega.

# Git hooks
Git hooks aise scripts hote hain jo specific Git events par automatically trigger hote hain. Yeh aapko Git workflow ke dauran kuch tasks automate karne ka option dete hain, jaise commit karte waqt ya push karte waqt koi extra check ya notification dena.
Types of Git Hooks:
- Client-side hooks: Yeh local actions ke liye hote hain, jaise commit ya merge karte samay. Example: Agar aap commit kar rahe hain, toh aap ek hook laga sakte hain jo check kare ki code ka style sahi hai ya nahi, aur agar sahi nahi hai toh commit rok diya jaaye.

Example: pre-commit hook
```
#!/bin/sh
if git grep -q 'debugger' .; then
  echo "Error: Debugger found in code!"
  exit 1
fi
```
- Server-side hooks: Yeh remote repository par push ya pull hone waale actions ke liye hote hain, jaise push hone par kuch policy check karna ya koi notification bhejna.

Example: post-receive hook
```
#!/bin/sh
echo "Push successful! Changes have been received by the server."
```
Jab bhi koi changes push karta hai server par, yeh hook ek message bhej sakta hai ya kisi external service ko notify kar sakta hai.

- Use Karne Ka Tarika:
Hooks ko .git/hooks folder mein rakha jata hai.
Agar aap koi hook enable karna chahte hain, toh us event ka naam rakh kar ek executable script likh sakte hain (jaise pre-commit ya post-merge).
Jab woh specific event hota hai, toh yeh script automatically run ho jaata hai aur aapka task complete karta hai.

File ko executable banana hota hai, jiske liye aap yeh command use kar sakte ho:
```
chmod +x .git/hooks/<hook_name>
```
# An Example Git-Enforced Policy
Git mein ek aisi policy establish karna jo commit message format ko check kare aur certain users ko specific directories ko modify karne se roke, bohot helpful hota hai. Yeh policy enforce karne ke liye hum client-side aur server-side hooks ka istemal karte hain.

Example Steps:
- Custom Commit Message Format Check: Hum ek pre-commit hook banate hain jo ensure karta hai ki commit message ek specific format follow kare, jaise JIRA-<number>: <message>.

pre-commit Hook Example (Ruby):
```
#!/usr/bin/env ruby

commit_message_file = ARGV[0]
commit_message = File.read(commit_message_file)

unless commit_message.match?(/^JIRA-\d+: .+/)
  puts "Error: Commit message must start with 'JIRA-<number>: <message>'"
  exit 1
end
```
Agar commit message sahi format mein nahi hai, toh commit reject ho jayega.

- User Permissions Check: Server-side, hum ek pre-receive hook banate hain jo check karta hai ki kya user ko specific subdirectory mein changes karne ki permission hai.

pre-receive Hook Example (Ruby):
```
#!/usr/bin/env ruby

STDIN.each_line do |line|
  old_rev, new_rev, ref = line.split

  if ref.start_with?("refs/heads/sensitive-directory")
    user = `git config user.name`.strip
    allowed_users = ["user1", "user2"]

    unless allowed_users.include?(user)
      puts "Error: You do not have permission to push to #{ref}"
      exit 1
    end
  end
end
```
Agar user sensitive-directory mein push karne ki koshish kare bina permission ke, toh push reject ho jayega.
