**NOTE: This guide has not yet been proofread, and is not even done. Just uploading it here now to keep it safe while I keep working on it.**
# Guide for setting up a dev enviroment to become credit to team.

Have you ever wondered what you could do to contribute to Castaway.tf?
One thing you could do, is become familiar with the coding (more like scripting really, but who gives a fuck? Normies certainly don't) aspect of Castaway.tf

**You too can become a keyboard slave!** 
Screaming into the night at compilation errors and help rectify the mistake that is Post-2013 Valve.

This tutorial will teach you several things (the basics mind you)
for getting setup.

* How to create a Github account
* How to install Git
* Setting up SSH key and testing connection to Github (Linux)
* The basics of navigating in a terminal
* Creating a repository (aka 'repo') in git.
* Your first commit
* Making a branch in git and using merge
* Creating a repo on Github and pushing to it.
* Fetching, merging from, or pulling from your remote.
* Rebasing a branch.
* How to install the TF2 dedicated server.
* How to install Metamod:Source and Sourcemod.
* How to fork the Castaway.tf repo.
* Dependencies to compile the reverts plugin.
* Compiling reverts.sp
* Overview of Castaway.tf work progress.
* Doing research.
* Back to git!
* Git tags? GIT TAGS!
* Pull Requests (Finally!)
* Closing words.

**It's important to know that this tutorial is not
for teaching you the basics of programming or programming mindset,
you will need to learn this elsewhere**

## How to create a Github account

First, you need a e-mail. 
If you don't have one, go make a proton one.
https://proton.me/

After you are done with that,
go register on github:

https://github.com/signup?source=login

After you are done creating a Github account, there's some additional things you want to do before we move on:

1. Click your avatar picture in the top right.
2. Select 'Settings'.
3. Fill out the public profile as you see fit. None of it is actually required. But can help, especially the Name field.
You can safely ignore the pronouns field, github is pozzed as fuck, but the Castaway.tf repo is on github so it is what it is.
4. When you are done (and if you changed anything) click the green button that reads 'Update profile'.
5. Click 'Emails' under the 'Access' section.
6. Look at 'Keep my email addresses private', there's a switch next to it to the right that is in position off, click it so it becomes on.
7. Ensure that it also flipped the new switch that appeared beneath it ('Block command line pushes that expose my email') to on.

Note: The reason we want those two switches turned to the ON position is because it hides the e-mail you registered with from the commits and pushes etc made on Github, this protects you from spam as long as you follow another important step later on in the Git guide.

8. (OPTIONAL BUT RECOMMENDED) if you want to increase the security of your github account further, I suggest adding 2FA, just be carefull so you don't loose access. It's done under 'Password and authentication'.
9. In the same box where you flipped the switch to ON, you should see a e-mail that is formatted like this: numbers+githubusername@users.noreply.github.com
You want to copy that e-mail and save it down somewhere. You will be using it when you configure git later, and it's also something you want to give out to the rest of us during development so you can be credit to team when you assist with stuff.

Now you have a github account properly configured and ready.
One more thing: go to Settings>Repositories
and change the default branch name from main to master then press the 'update' button, then wait for the tiny message and then press the 'update' button one more time. You want to see a message at the top that says 'New repositories you create will use 'master' as their default branch name. '. We do this to not feed the retarded DEI bullshit.

## How to install git

In order to be able to contribute to the castaway.tf repo, you will need a software called git.
It was written by a very cool nerd from Finland (Perkele) called Linus Torvalds for version control for the Linux Kernel. He's pretty based all things considered since he only cares about merits and hates retards.

It has proven invalueable to basement dwelling nerds for many years now, and it will be of use to you too.

At this point, the tutorial will split up into Windows
and Linux specific points, and they will merge and diverge as needed as some commands and steps are for a specific OS, and others can be used on both.
The tutorial assumes that people on Linux are more capable of less handholding as there's already plenty of tutorials and examples online.

### Linux
Git is almost always already installed with your choosen distro already, if it's not, you can get it here:

https://git-scm.com/install/linux
Use the appropiate command for your distro.

### Windows

Windows have a fairly easy time getting setup with git.
Begin by visiting this link:
https://git-scm.com/install/windows

You want `Windows/X64`
Run the installer, and click next on everything besides two things:

When the installer asks you about what editor to use for git, I suggest
notepad. Every Windows user has Notepad. You can ofc choose something else
but this tutorial will not focus on that. What it means is that
when you for example need to resolve a conflict in git (more on that later), git will open your chosen editor to do stuff in.

Another thing the installer will ask you about is the default branch name,
You want to select the option that allows you to set your own, and ensure it says `master`.

When you are done with the install, open the Windows Start Menu and start typing 'Powershell'. Start Powershell.

Type the following command into the terminal:
`git --version`

You should get a positive reply with the version of git.

(For Linux), we want to ensure you don't get 
infected with the DEI mindvirus whenever Git 3.0 comes out in the future, run this command in a terminal:

`git config --global init.defaultBranch master`
This sets the default branchname to master, which is what proper people will have for their repositories. Only a faggot would willingly let insane trannies dictate to them what and how their tech is to be used (I'm not joking, that faggot who tried to implement the CoC (Code of Conduct) onto Linux and places like Github is a literal insane tranny groomer).

Being proper people, we will not allow that bullshit.

The next section 'Setting up SSH key and testing connection to Github (Linux)' is specifically for Linux, Windows peeps can skip to `The basics of navigating in a terminal`, as we will deal with the setup of authentication for Windows users in the "Pushing" part of the 'Comitting, pushing, merge in git'.

## Setting up a SSH key (Linux)

The easiest way for a Linux user to authenthicate themselves to github is by setting up a SSH key.

Begin by running this command in a terminal:

`cd ~/.ssh`
then
`pwd`
You want to ensure that the path is:

/home/yourusername/.ssh

Now follow these steps:

1. `1. ssh-keygen -t ed25519 -C "numbers+yourgithubusername@users.noreply.github.com"`
You want to replace the example e-mail
with the noreply e-mail you got from the Emails step of 'How to create a github account'. This allows you to identify what this key is for later.

2. You will now be prompted with something like
`Enter file in which to save the key (/home/yourusername/.ssh/id_ed25519):`
The default key is only something you'd want to use globally.
You should give it a proper name. Something like
`mykeyghctf` or anything you want really.
Note: If for some reason you ignored what I said about using cd to get into the .ssh folder first, you will want to enter the full path of the file you intend to create.
With the example given, that would be `/home/yourusername/.ssh/mykeyghctf`

3. You will now see the following: `Recommended: set a passphrase.`
I do recommend you set a passphrase, this is not like your typical password where you'd want something with 40+ chars or whatever. 6 basic words and some ! and ? sprinkled into it will do just fine if it helps you remember it. This is because the intent is to delay any thief so you have the time to revoke the key from the services you use it on.

4. After you are done setting the passphrase, you will se a bunch of stuff, including a "visual art", this visual art does not need to be saved down.

5. Now proceed to enter this command `eval "$(ssh-agent -s)"`.
What it does is that it will launch a ssh-agent to handle your ssh keys for this current terminal. Since it's likely that you are using a Desktop enviroment, it means that it will only be active for this current session (aka this current terminal window).

6. Now run this command: `ssh-add ~/.ssh/yourcodekeyname`.
What that does is add the ssh key you have created. Do not add the .pub file of the same name! That file is what you give to the services you want to authenticate yourself against.

7. You will be asked for the passphrase you used (if you set one). This only needs to be entered once per terminal window/session you run step 5 and 6 in. There are ways to make it less painful, but I won't go trough it in this tutorial. Depending on how seriously you want to take your security, it's just a good idea overall to NOT make the ssh agent enable on all terminals automatically once per user login. But you do you.

8. Go to the .ssh folder of your user, find the keyname.pub you created, open it with your preffered editor. Copy all the text inside of it. Make damn well sure you are not copying from the keyname file, it MUST be the one file that ends in .pub !!!
The one without .pub is the private part of your key and must not be shared with ANYONE! Giving anyone else that file or its contents would be like going to the darkest streetcorner and handing over the keys to your house while wearing a "Dunce" cap.

9. If you are not still in Settings on github, click your profile avatar to the top right, then Settings, then go to 'SSH and GPG keys'.

10. In there, click the green 'New SSH key' button.

11. You will see three fields: 'Title', 'Key type' and 'Key'.
In the 'Key' field, paste in all the text you copied from
the .pub file, ensure that 'Key type' is set to 'Authentication Key', then give it a sensible name.
When you are done, press the green 'Add SSH key' button.

12. Now, we want to add Githubs own public key to our system. One can elect to just answer "Yes" to the question that pops up in the terminal to trust the unknown certificate, but that's crazy stuff. Visit https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints

13. In the .ssh folder of your user, create a file called "known_hosts" if it does not already exist. No .txt or other silly file endings! Then open it with a text editor.

14. In that weblink you just visited, you should see this text and a box below it:
`You can add the following ssh key entries to your ~/.ssh/known_hosts file to avoid manually verifying GitHub hosts:`

You want to copy all the text inside of that textbox, paste it as is into the known_hosts file you made, and then save it.

15. Finally, run this in the same terminal that you did step 5 and 6 in: `ssh -T git@github.com`

16. If you have done all the steps correctly, you should see this text in the terminal:
`Hi YourGithubUserNameHere! You've successfully authenticated, but GitHub does not provide shell access.`

If so, you have everything you need for later when we will work with git on pushing things to github. Good job!

## The basics of navigating in a terminal.

There's really only 3 commands which is of interest to you right now. All of whom can be replicated with the GUI, but sometimes it's simply faster to use a terminal.

`cd`,`ls` (ls can be used on Powershell too on Windows, but more oldschool or if you insist on using cmd would be `dir`) and `mkdir`.

`cd` allows you to change your working directory.

A working directory looks like this:

Windows: C:\Users\YourUserName\
Linux: /home/yourusername/

Note: Before we continue, notice how paths differ in Linux compared to Windows. Linux generally do not make use of Drive-Letters like `C:`, and the path seperator is `/` instead of `\`.

Another thing to keep in mind is that Windows does not care about CaSe-SenSiTivity in paths and filenames. Linux absolutely does. Also Linux tolerates more symbols in the filenames and foldernames.
When you work on the Castaway.tf repo later, do not use BIG LETTERS in the folder and filenames, and stick to `A-z`,`1-9`,`-`,`_` and `.`.
No spaces either in folder and filenames! It makes it much harder for scripts to get things done.

### back to cd
Let's continue with the `cd` command.
You can type either a foldername that you know in your current working directory, or a entire path to wherer you want to go.

For example, if you typed
Windows: `cd C:\Users\YourUserName\Downloads`
Linux: `cd /home/yourusername/Downloads`

You'd end up in the Downloads folder for your user.
Your typical Terminal in Linux and Powershell in Windows
also have the ability to autocomplete path and filenames.

For example, let's say you have a folder named 'myreallycoolstuff' in the Downloads folder.
You could while you have your working directory set to the Downloads folder just type `myreally` and then press the TAB button (⇄) and the terminal and powershell will just autofill the rest for you. Unless you have more folders or files that start with the same name, then you need to give it a bit more, perhaps `myreallyc`.

Hot Tip: The Terminal in Linux often don't (depending on configuration) show you the entire path at all times like 
Powershell does. While you look for settings to change that (if you like to do that), you can type the command `pwd`
to get the entire path of your current working directory on Linux.

Another thing you can do with cd is a short command to go back (formally: Up a level) a folder.

Try typing `cd ..` into the Terminal/Powershell.
You should now be at `C:\Users\YourUserName`, `/home/yourusername`.

You can even jump several times in one command, seperating each with the appropiate path seperator:

Windows: `cd ..\..`
Linux: `../..`

That would go back 2 folders, meaning you'd end up at
`C:\Users` and `/home` respectively.


Note: If your path contains s p a c e s, at any point, you need to sorround the path with "" like this:

Windows: `cd "C:\Users\YourUserName\Downloads\My Folder"`
Linux: `cd /home/yourusername/Downloads/My Folder`

Make a effort to avoid ever having spaces in your paths.
### ls

ls is a very usefull command for listing the current folders and files of your current working directory.

Linux: 
* Only normal files and folders, not hidden ones `ls -l`
* Both normal and hidden files and folders, `ls -la`
Windows: 
* Only normal files and folders, not hidden ones `ls`
* Both normal and hidden files and folders, `ls -Force`

Windows also has the dir command. If you need
hidden, add the /a flag: `dir /a`.

### mkdir
`mkdir` is used to make a new directory/folder.
Example: `mkdir myawesomefolder`.
The folder will be created in your current working directory.


This is all you need for navigation and basic folder creation, I'm intentionally NOT teaching you about
modifying permissions and deleting files/folders,
you will have to go read about that on your own.
This is even more important on Linux,
running `rm`,`mv` or `dd` without knowing what you are doing
can lead to catastrophic irreversible data loss. Stick to the GUI for now when you need to delete, move or rename stuff.

## Creating a repository (aka 'repo') in git.

It's time to start learning how to use Git.

### Folder structure
1. Start by using the `cd` command to move into your user folder, then the `Documents` folder.

2. When there, make a folder named 'castaway', we will be using this folder for the rest of the tutorial.

3. cd into that folder and create these two folders: 'tf2-server' and 'repos'

4. cd into the 'repos' folder.

5. make a folder named 'mytestrepo' and cd into it.

Unless you are told to change otherwise, you current working directory should be:

Windows: `C:\Users\YourUserName\Documents\github-repos\mytestrepo`
Linux: `/home/yourusername/Documents/github-repos/mytestrepo`

### Initializing a git repo.

While in the mytestrepo folder, run this command: `git init`.
This will create a git repository inside of your folder.
Fairly short chapter really.

## Your first commit.

Now follow along:

Using your favorite text editor (Notepad is fine for these basic tasks on Windows, pick something appropiate on Linux), create
a file named 'MyTestFile.txt'.

Remember how I told you that normally you should avoid BIG LETTERS to make it easier for Linux? This is not a iron clad rule depending on the kind of programming that's being done, especially not for files. I did say to try to avoid it to avoid confusion. In our specific example,
we are essentially using CamelCase for the filename.

Enter the following into the text file:

`Hello World!`.

Save the file as a normal .txt file.

As we go along in this tutorial, OS agnostic commands such as git
commands will be noted as COMMAND: instead of the typical 
windows path or user@domain printout you might see in a terminal
when it's ready to accept a command from you.

Now in your terminal, type `git status`.

```
COMMAND: git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        MyTestFile.txt

nothing added to commit but untracked files present (use "git add" to track)
```

`git status` is a command you will be using ALOT to check the status of your git repo so you avoid doing catastrophic things.

Looking at what git replied with:

'On branch master', this simply tells you that you are currently on the branch master.

'No commits yet', this tells you that the branch has no commits on it yet, which is to be expected since the repo was just recently made.

'Untracked files:'

Here, git is telling you that there's untracked files in the same folder as the git repo.

Before we continue: many repos make use of something called .gitignore to ensure that files not strictly needed to compile a project is included as untracked files, modified files etc, these can be things like editor settings for a IDE, or in castaway.tf's case, things like the default plugins and include files that come with Sourcemod, this tutorial will not go trough .gitignore besides knowing how to work with the specific one Castaway.tf has in order to add new files, something you will rarely if ever need in the first place. Go find a tutorial on the internet if you want to know more about .gitignore.

Moving on...
Git also tells you 
'nothing added to commit but untracked files present (use "git add" to track)'.

What this means is that nothing has been added that could be commited, but that untracked files are present.

It also helpfully gives you the command you need to add untracked files.

Do so. run the command `git add MyTestFile.txt`.

This will result in the following:

```
COMMAND: git add MyTestFile.txt
COMMAND: git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   `MyTestFile.txt
```

You should always run `git status`
after important operations like adding or removing files, before a push, before a checkout, and when adding new files.

Especially now when you are new, and even if you are not, at the very minimum do it before you try checking out a branch (more on that later) and before pushing (more on that later also).

You can undo the decision to add the file with the command git suggested, but we won't be doing that.

The process we have done so far with git status to check the status of the repo, and specifically by adding new, modified or deleted files and folders etc is formally called 'staging'.

The tutorial will henceforth use 
"Stage the files" or "Unstage the files"
and so on.

Staging is the first of 3 steps in the formal process of using git to exercise version control onto a collection of files in a folder.

Before we continue, the repo needs to
know who is going to be comitting the staged changes.

Get your github noreply e-mail ready, because we will be using it.

The first command:

`git config user.email ""`
Will set the email of the commiter on this repo. You want to enter the github noreply email you aquired into the ""
so the command looks like this:

`git config user.email "numbers+githubusername@users.noreply.github.com"`

Where the e-mail is the noreply email of your github account that you saw in step 9
of 'How to create a Github account' chapter.

`git config user.name ""`
Set the name that will be displayed on the commit. Here you want to set it to the same you have on Github, if you did not set a specific name in the Profile in Settings on Github, use the github account name. You can technically use whatever you want here, but please be consistent.

With these things done, you are now ready to commit your staged changes:

`git commit -m "Initial commit."`

This will create a commit (a 'snapshot' if you want to use another name for it. But formally it's called a commit and it's what the tutorial will use) of the state of all the tracked files at that particular point in time.

### Logs everywhere!
You can see a log of all the commits
on the current branch you are on
with `git log`.

A couple of usefull variants on git log:

`git log -x` Replace x with how many commits back you want to look.
`git log --oneline` Makes the log nicer to look at. One commit per line.

`git log --oneline -x` Same idea as 
the other with -x, allows you to look back x number of commits.

`git log --since="2026-02-01" --until="2026-02-10"` Allows you to see commits made between two dates.

`git log --oneline --since="2026-02-01" --until="2026-02-10" -10` Same, but with the nice oneline stuff.

More ways to use logging can be found in the git book:
https://git-scm.com/book/en/v2

## Making a branch in git and using merge
One of the most primary ways you will be working with git, is with branches.

So to begin with: 'master' is also technically a branch, it's just the first branch that we plan to use as the primary branch of the repo.

If you imagine a endless tree, then master would be the main trunk, the branches are offshoots that are based on the trunk at that particular point (commit) in time, and then these branches come back into the trunk later on when they are ready to be merged, becoming part of the trunk.

### So what is a branch?
A branch is a diverging point usually based on another branch for the purposes of developing one or more features without disturbing the branch it was based on.

This allows people to co-operate on developing the software without interrupting eachother. When things go well, this can lead to a situation where there are no so called 'conflicts', allowing branches to seamlessly be merged into master. And if a conflict DOES appear, git provides tools and solutions to resolving these conflicts.

Creating a new branch based on master (or based on any branch really) is done by using the `git checkout` command. This command normally checks out a certain branch (which typically will be the latest commit that branch has), but by passing a flag to the command, we will instead create a new branch (check git status first and ensure you are on master):

`git checkout -b mytestbranch`
This creates a new branch called 'mytestbranch', based on whatever branch you are currently on.

At the same time, it also checks out this new branch for you, which means you have now switched branch from 'master' to 'mytestbranch'.

Type git status and you should now see this:

```
COMMAND: git status
On branch mytestbranch
nothing to commit, working tree clean
```

As you can see, we are now on the mytestbranch. 

At the moment, this branch is on the same commit as the last one you had on master. If you run the command `git log --oneline` you will see the following:

```
COMMAND: git log --oneline
2c3b723 (HEAD -> mytestbranch, master) Initial commit.
```

The HEAD -> shows you what branch you are currently on, and any other branches that has the same commit is also shown. Here we see master.

Let's try making a new commit on this branch to see how it changes.

Open your MyTestFile.txt file and add this line:
'And welcome to'

Save the file, and like you learned before in 'Your first commit', make a commit. When you make commits,
they should be short and descriptive of what changes the commits do.
For this example tutorial, I suggest a message like
'Added a new line of text to file MyTestFile.txt'.

Note:
If you are working with several files in the same commit (more than 2), you could do something like 'Added new lines of text to .txt files in folder X.'
and urge people to look at what files are touched by the commit. 

After having committed the file, do the following:

```
COMMAND: git log --oneline
0ad6152 (HEAD -> mytestbranch) Added a new line of text to file MyTestFile.txt
30dc0c6 (master) Initial commit.
COMMAND: git checkout master
Switched to branch 'master'
COMMAND: git log --oneline
30dc0c6 (HEAD -> master) Initial commit.
```

As you can see, our branch mytestbranch has now moved ahead of master (as in the commit on mytestbranch is newer than the commit on master).

### Merging a branch in git

Now, considering that master is our primary branch, how exactly do we get the changes that we made in the mytestbranch into master?

We merge it in.

First, we need to check out master:

`git checkout master`

(Before we continue on, now take a look at the MyTestFile.txt, you should see the text 'And welcome to' disappear, this is because we checked out master, which is on a older commit).

Now, while you are on master, type this:

`git merge mytestbranch`

This will result in the following:

```
COMMAND: git merge mytestbranch
Updating 30dc0c6..0ad6152
Fast-forward
 MyTestFile.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
```

(Note: You may not see the exact numbers here as I was messing with the file, that's fine).

We have now merged the changes from mytestbranch into master.

“Merge? But it says Fast-forward?”

This can look confusing at first. Since master had not changed since we started working on mytestbranch, there was nothing to combine.
Git simply moved the master branch forward to the same commit as mytestbranch.
This is called a fast-forward merge.

When master has changed, Git creates a new commit to join the two branches.

In some cases, a merge may result in a conflict that Git cannot solve automatically.
We will go through what conflicts are much much later in the tutorial.

Now, if you look again in notepad, you will see that the line 'And welcome to' has re-appeared while you have the 'master' branch checked out.

Also let's check the logs:

```
COMMAND: git log --oneline
0ad6152 (HEAD -> master, mytestbranch) Added a new line of text to file MyTestFile.txt
30dc0c6 Initial commit.
```
Now master is on the same commit as the one you made in the 'mytestbranch'.

When you work on the Castaway.tf repo, you will NEVER be using merge on the 'master' branch yourself since random owns the repo. Only random may merge code into master. You should NEVER do it unless you are updating your local 'master' in the Castaway.tf fork you made. More on how to work with the Castaway.tf repo later.

## Creating a repo on Github and pushing to it.

For Linux Users: Make sure you followed all the steps in the 'Setting up SSH key and testing connection to Github (Linux)'
chapter before continuing.

We need a server to "push" to.
In our case (and since you will be using Castaway.tf's Github repo later on), it will be a repo on Github. That's why we spent time early on preparing by creating a Github account etc.

The idea is that you have a local repo where you code, and a remote repo that we push the local commits and branches to for storage and so others can see it, review it, clone the repo or whatever.

When you work on your own project (or fork), it's so called "online" is often called "origin". When you fetch/pull from the original project that you forked from, we call that "upstream". Generally unless you are a maintainer or own the upstream repo (which would be called origin for you), you never push to it (nor would it allow you to do it unless you have the permissions for it).

To use the example of Castaway.tf:

randoms repo is the upstream.
your fork of it that you have on your github account is origin.

To begin with, you need to add some 'remotes' to push and fetch from.

Click on your avatar in the top-right
and then click 'Repositories'.
Then click the green 'New' button.

* In 'Repository name', fill in 'mytestrepo'.
* In Description, fill in whatever you want or leave it empty.

Make NO other changes to the configuration (this includes making sure Add README is set to off, we do not want to generate a README.MD for this tutorial so we ensure we have a clean repo).

Click 'Create repository'.
Wait a second or two, then
look in the box that says
`…or push an existing repository from the command line`.

In that box, copy the first command (DO NOT COPY AND PASTE ALL COMMANDS AT ONCE, GITHUB IS RETARDED). We will be pasting it in into a terminal soon.

In your local git repo, ensure you have 'master' checked out (remember? `git status` to check what branch you are on. You can also use git branch and check which one has a * on it, but it's better to check with git status to ensure working directory is clean),
then paste in the 'git remote add ...'
command you got from the box.

After that, type in this command:

`git remote -v`

This will show you the remotes added to this local repo. You should see this if you did this correctly:

```
origin	URL_HERE (fetch)
origin	URL_HERE (push)
```
And the 'URL_HERE's replaced with the URL
you saw in the box on github after creating the repo

If you do, good job.

### Preparing for push.

Now that the remote has been added, we can prepare for pushing.

For Linux users, you should already be set up for pushing, but if you came back to this tutorial later and have closed the terminal or logged out of your user, go back to Step 5, 6, and 7
of the 'Setting up SSH key and testing connection to GitHub (Linux)' chapter
and ensure your terminal is set up with an SSH agent and that you have added your key to the agent.

First, make sure you have the 'master' branch checked out.
Then run the command 'git status'.

You want it to read the following:

git status
On branch master
nothing to commit, working tree clean

When you are on the correct branch you want to push, have nothing to commit, and the working tree is clean, only then should you push.

Enter this command (and Windows users, you will now go through your part of setting up authentication when you run the push command; for Linux users, move on to 'After the push').

`git push -u origin master`

### Authentication on Windows

Now for you Windows users, you will see a credentials manager pop up.
I recommend using 'Sign in with your browser'; it will open the web browser that Windows has set as standard.

Follow these steps:

1. Click 'Sign in with your browser'.
2. In the browser tab that pops up, you might be prompted for your GitHub username (or email)
   and GitHub password if you are not already logged into your GitHub account in that browser.
   Enter the details and press 'Log in'.
3. You will see a page that says 'Authorize Git Credential Manager'.
4. Change nothing; just click 'Authorize git-ecosystem'.
5. When it says 'Authentication Succeeded', you can do what it says and close the tab.

You are now done with authentication for this computer/Windows account.

If your local (or Windows) computer account, or the computer itself, is compromised for any reason,
or if you reinstall Windows or similar, you can revoke the authentication for that device by going to
'Settings' in your GitHub account. From there, go down to 'Applications' in the 'Integrations' section,
then to 'Authorized OAuth Apps'. There you can revoke access for 'Git Credential Manager'.

### After the push

You should now see the following:

```
COMMAND: git push
info: please complete authentication in your browser...
git: 'credential-manager-core' is not a git command. See 'git --help'.
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 6 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 331 bytes | 331.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/yourgithubusername/mytestrepo.git
   74edd4d..f56df87  master -> master
```

(Small note: that `git: 'credential-manager-core' is not a git command. See 'git --help'` seems to be a small error/config error with my install, it might not show up for you)
You might see slightly different numbers here, it does not matter too much (especially when it comes to the hashes).

You have now successfully pushed to your repository on GitHub.
Go to it on GitHub and you should now see your 'MyTestFile.txt' appearing.
The branch on GitHub will be 'master'.

Let me briefly explain what the push command did, since this will matter when we later fetch and merge changes.

The -u switch tells Git:
'Remember that the upstream for this local 'master' branch is the branch named 'master' on the remote called 'origin'.'

'origin' is the remote label (remember how we created it earlier using 'git remote add').

And 'master' is the local branch we wanted to push.

When you run the push command for the first time, Git connects to GitHub and creates a real branch named 'master' on the remote repository, because it does not exist there yet.

At the same time, Git also creates or updates a local remote-tracking branch called 'origin/master'.
This branch exists only in your local repository and represents Git’s last known snapshot of the remote 'master' branch.

The local 'master' branch is your working branch.
The local 'origin/master' branch is read-only and is only updated when you run 'git fetch' or 'git pull'.

Because we used the -u switch, Git now knows that your local 'master' branch is associated with the remote 'master' branch on 'origin'. This means that in the future, while the 'master' branch is checked out, you no longer need to specify the branch name explicitly.

You can simply run:

'git push'

Git will then automatically push your local 'master' branch to the remote 'master' branch on GitHub.

## Fetching, merging from, or pulling from your remote

Git is not only about pushing. You also need to fetch changes from the remote repository (often to update 'master') and then merge them (or pull, if you are confident), so you can work with the latest state of the repository.

One of the ideas behind Git is that you do not have to constantly update just to continue working on your own feature. However, sometimes it is simply necessary to do so.

For example, if a function’s name and/or parameters are changed in 'master' and you want to avoid hearing 'please rebase on master' from the original repository owner, the first thing you should do is make sure you are up to date before creating your pull request.

To that end, let’s walk through how fetching and updating works in practice.

We will need something new to fetch, so we will modify 'MyTestFile.txt' directly on GitHub to make some changes happen.

Click on 'MyTestFile.txt' in your GitHub repository in the web browser.
Then click the small pen icon (it is near the 'Raw' button).

This opens GitHub’s online text editor.

Now add the following new line of text:

'the Dominatening!'.

Then click the green button that says 'Commit changes...'.

Keep the commit message as-is.
In the description field, type 'Added a new line.'.
Then press the green 'Commit changes' button.

Now go back to your terminal and run the following two commands:

'git fetch'
and then
'git status'.

You will see the following:

```
COMMAND: git fetch
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1008 bytes | 50.00 KiB/s, done.
From https://github.com/ỳourgithubusername/mytestrepo
   0e29fb4..43f7d1b  master     -> origin/master
COMMAND: git status
On branch master
Your branch is behind 'origin/master' by 1 commit, and can be fast-forwarded.
  (use "git pull" to update your local branch)

nothing to commit, working tree clean
PS C:\Users\GotMitUns\Documents\testrepo>
```

git fetch does the following:

It contacts the remote repository and updates your local remote-tracking branches (for example, 'origin/master') with any new commits found there.
Crucially, it does not apply those changes to your local working branch (such as 'master').

Which remote is fetched depends on your configuration. In the common case where you have only one remote and an upstream set, git fetch will fetch from that remote automatically. You can check which remotes are configured with:

`git remote -v`

If you have several remotes (which I will go through later for the Castaway.tf repository, especially if you prefer doing more work from the terminal and only using GitHub for PRs later), it is often better to be explicit and run:

`git fetch origin`

This ensures you are fetching from 'origin' specifically, rather than fetching from all remotes or relying on implicit defaults.

After fetching, Git may tell you that your local branch is behind the remote-tracking branch. For example, it may say that your local 'master' is behind 'origin/master' by one commit. This means new commits exist on the remote, but they have not been applied locally yet.

Before doing what Git suggests, you may want to inspect the changes first.

You can do so with:

`git diff master..origin/master`

This shows the differences between your local 'master' branch and 'origin/master'.
Be careful when using this command directly: on a branch like 'master', this can produce a lot of console output — potentially thousands of lines in large projects.

To make this more manageable, start with a summary view:

`git diff --stat master..origin/master`

This shows only which files changed and roughly how large those changes are.

If even that is too noisy because many files were touched, you can reduce it further to just filenames:

`git diff --name-only master..origin/master`

If you want to inspect a specific file in detail, you can do so like this:

`git diff master..origin/master -- path/to/filename`

You can obtain the correct paths from the output of the --name-only command shown above.

If everything looks good and you are satisfied with the changes, you can merge them into your local branch with:

`git merge origin/master`

This merges the already-fetched changes from the remote into your local 'master'.

You should only use git pull when it is your own repository that you fully control, or when you explicitly do not care about inspecting changes first. This is because git pull performs a fetch behind the scenes and then immediately applies the result. In addition to being ambiguous when multiple remotes are involved, it can also fetch and apply new commits that you did not inspect or plan for.

## Rebasing a branch

Finally, we come to one of the most important commands you will use when working with the Castaway.tf repo: **rebase**.

It can sometimes take a while for *random* to review and accept a pull request (PR). While you are waiting, other people are still working on the repo. That means the **master** branch can (and often will) move forward while your branch stays where it is.

This is normal — and it is exactly why rebasing exists.

---

### What does it mean that “master moved ahead”?

Let’s say you create a branch called:

`revert/hurtfallsound`


This branch is based on **master** at a specific commit. To keep things simple, let’s call that commit **M100**. M will be master's commits and B will be the commits on your branch.

You start working and make some commits on your branch:

`B101, B102, B103, B104, B105`

Your branch now looks like this:

`M100 ─ B101 ─ B102 ─ B103 ─ B104 ─ B105`

While you are working, other people continue committing to **master**. Master now has two new commits:
`M101, M102`

So master looks like this:
`M100 ─ M101 ─ M102`

Your branch is now **behind** master.
More accurately, you might see something like this in github (not git):
`This branch is 5 commits ahead, 2 commits behind githubuser/reponame:master`.

---

### What happens if you don’t rebase?

If you open a pull request without rebasing, your branch is still based on **M100**.

Git now sees two different histories that split at the same point:

```
master: M100 ─ M101 ─ M102
your branch: M100 ─ B101 ─ B102 ─ B103 ─ B104 ─ B105
```

At this point, merging becomes messier than it needs to be. This often leads to:

- confusing history.
- unnecessary merge commits.
- extra work for the maintainer.

This is why you will often see comments like:

> “This branch needs a rebase.”

---

### What rebasing actually does

When you **rebase** your branch onto the latest master, Git does something very simple conceptually:

> It takes *your commits* and replays them **on top of the newest master commit**.

After rebasing, the history becomes:
`M100 ─ M101 ─ M102 ─ B101 ─ B102 ─ B103 ─ B104 ─ B105`

Ideally, when you use interactive rebase in order to squash commits etc, it would look like this:

`M100 ─ M101 ─ M102 ─ B105`

So when the maintainer merged your branch into the original repo master,
it will end up looking like this:
`M100 ─ M101 ─ M102 ─ M103` where M103 = B105.

Where B105 was the final commit you tested yourself to the point where you feel it's ready for a pull request (or if you already made the pull request while master was still only on
M100 and then it moved on to M102).

Nothing from master is lost. Your work is simply moved so it now comes **after** the latest master commits.

This makes the pull request clean and easy to merge.

---

### Why this matters in practice

Castaway.tf is worked on by multiple people at the same time. Rebasing ensures that:

- your work is based on the **latest** code
- no one else’s changes are accidentally overridden
- the project history stays readable and linear

Because of this, it is a good habit to:

> **Always check if you need to rebase before opening a pull request.**

You can do this by:
- looking at the commit history of `master` on GitHub
- checking whether new commits were added after the commit your branch was created from

---

### Rebasing and “trash commits”

When working on a feature, it is completely normal to make a lot of temporary or messy commits while figuring things out.

However, a pull request full of “trash commits” can make reviews harder and distract from what actually changed.

This is where **interactive rebase** comes in.

Before opening a PR, you can:
- squash commits
- reorder them
- fix commit messages

The goal is not to hide mistakes — it is to present your work in a way that is easy to review.

Ideally:
- your commits show meaningful steps
- any follow-up commits are responses to review feedback

More eyes on the code means more bugs caught — and a cleaner history helps everyone.


To that end, we will run a script in order to help prepare a branch for you
for a silly (but real) scenario.

### Preparing a branch for rebase.

1. ensure that MyTestFile.txt contains exactly the text as it should
if you have followed the tutorial so far:

```
Hello World!
And welcome to
the Dominatening!
```

If it does not, if it contains a empty line before and after etc, then while on the master branch, use notepad/nano or whatever text editor you have and ensure the .txt file contains
exactly the text, then save the file and make a commit on the master branch so it's prepared properly.

2. Create a new branch based on master named 'rebasetest'.

3. Pick the correct script according to your OS.


Linux:

```
#!/bin/sh
set -eu

EXPECTED_REPO_NAME="mytestrepo"
EXPECTED_BRANCH="rebasetest"
SLEEP_SECONDS=2

REPO_PATH="${1:-}"
FILE_PATH="${2:-}"

if [ -z "$REPO_PATH" ] || [ -z "$FILE_PATH" ]; then
    echo "Usage: $0 <path-to-repo> <file-path-in-repo-root>"
    exit 1
fi

# Resolve repo root
REPO_ROOT="$(cd "$REPO_PATH" && git rev-parse --show-toplevel 2>/dev/null)" || {
    echo "ERROR: Not a git repository: $REPO_PATH"
    exit 1
}

REPO_NAME="$(basename "$REPO_ROOT")"
if [ "$REPO_NAME" != "$EXPECTED_REPO_NAME" ]; then
    echo "ERROR: Repo is '$REPO_NAME', expected '$EXPECTED_REPO_NAME'"
    exit 1
fi

CURRENT_BRANCH="$(git -C "$REPO_ROOT" rev-parse --abbrev-ref HEAD)"
if [ "$CURRENT_BRANCH" != "$EXPECTED_BRANCH" ]; then
    echo "ERROR: On branch '$CURRENT_BRANCH', expected '$EXPECTED_BRANCH'"
    exit 1
fi

FILE="$REPO_ROOT/$FILE_PATH"
if [ ! -f "$FILE" ]; then
    echo "ERROR: File does not exist: $FILE_PATH"
    echo "Refusing to create new files. Exiting."
    exit 1
fi

commit() {
    git -C "$REPO_ROOT" add "$FILE_PATH"
    git -C "$REPO_ROOT" commit -m "$1"
    sleep "$SLEEP_SECONDS"
}

replace_line_5() {
    NEW_LINE="$1"

    awk -v repl="$NEW_LINE" '
        NR==5 { print repl; next }
        { print }
    ' "$FILE" > "$FILE.tmp"

    mv "$FILE.tmp" "$FILE"
}

# ---- first commit: force exactly one blank line + broken line ----
awk '
{ print }
END {
    print ""
    print "Match begns in 10 seconds!"
}
' "$FILE" > "$FILE.tmp"

mv "$FILE.tmp" "$FILE"
commit "initial commit on branch rebasetest"

# ---- Replacing line 5 steps ----

replace_line_5 "Match begins in 10 secods!"
commit "typo fix? fuck why is it not working"

replace_line_5 "match begins in 10 seconds!"
commit "case tweak maybe?"

replace_line_5 "Match begins in ten seconds!"
commit "words vs numbers? idk"

replace_line_5 "Match begins in 10 seconds!"
commit "Added a new line to MyTestFile.txt"

echo "Script is done!"
```

Windows:

```
param (
    [Parameter(Mandatory=$true)]
    [string]$RepoPath,

    [Parameter(Mandatory=$true)]
    [string]$FilePath
)

$ErrorActionPreference = "Stop"

$expectedRepoName = "mytestrepo"
$expectedBranch   = "rebasetest"
$sleepSeconds     = 2

# Resolve repo root
$repoRoot = git -C $RepoPath rev-parse --show-toplevel 2>$null
if (-not $repoRoot) {
    throw "Not a git repository: $RepoPath"
}

$repoName = Split-Path $repoRoot -Leaf
if ($repoName -ne $expectedRepoName) {
    throw "Repo is '$repoName', expected '$expectedRepoName', please check the path you gave. The reponame is whatever your git repo folder is and it should be '$expectedRepoName'."
}

$currentBranch = git -C $repoRoot rev-parse --abbrev-ref HEAD
if ($currentBranch -ne $expectedBranch) {
    throw "On branch '$currentBranch', expected '$expectedBranch', have you created '$expectedBranch' and is it based on master and is it checked out?"
}

$file = Join-Path $repoRoot $FilePath
if (-not (Test-Path $file)) {
    Write-Error "File does not exist: $FilePath"
    Write-Error "Refusing to create new files. Exiting."
    exit 1
}

function Commit-Step($message) {
    git -C $repoRoot add $FilePath
    if ($LASTEXITCODE -ne 0) { throw "git add failed" }

    git -C $repoRoot commit -m $message
    if ($LASTEXITCODE -ne 0) { throw "git commit failed" }

    Start-Sleep -Seconds $sleepSeconds
}

function Replace-Line5($text) {
    $lines = Get-Content $file

    # Ensure the file has at least 5 lines
    while ($lines.Count -lt 5) {
        $lines += ""
    }

    $lines[4] = $text   # line 5 (0-based index)
    Set-Content $file $lines
}

# ---- first commit: force blank line + broken line as lines 4 and 5 ----
$lines = Get-Content $file

# Ensure at least 3 lines (sanity; should already be true)
while ($lines.Count -lt 3) {
    $lines += ""
}

# Ensure line 4 is blank
$lines += ""

# Line 5: broken message
$lines += "Match begns in 10 seconds!"

Set-Content $file $lines
Commit-Step "initial commit on branch rebasetest"

# ---- Replacing line 5 steps ----

Replace-Line5 "Match begins in 10 secods!"
Commit-Step "typo fix? fuck why is it not working"

Replace-Line5 "match begins in 10 seconds!"
Commit-Step "case tweak maybe?"

Replace-Line5 "Match begins in ten seconds!"
Commit-Step "words vs numbers? idk"

Replace-Line5 "Match begins in 10 seconds!"
Commit-Step "Added a new line to MyTestFile.txt"

Write-Host "Script is done!"
```

4. In your favorite text editor, paste in the script.
If you are using Notepad to create the script on Windows. Ensure filetype
is set to "All Files" and ensure the filename is prep_rebase.ps1
before you save it, otherwise it does not become a script, but just a normal .txt file.
On Linux, the script should be named prep_rebase.sh

4. After that, open a new terminal at the location of the script
and run it like this (do not run any commands on your repo in the other terminal while the script is running,
let the script finish properly):

Linux (you may need to grant the .sh file the permission to execute as script, search the web):

`./prep_rebase.sh ~/Documents/github-repos/mytestrepo MyTestFile.txt`

Windows:

`powershell -NoProfile -ExecutionPolicy Bypass -File .\prep_rebase.ps1 C:\Users\YourUserName\Documents\github-repos\mytestrepo MyTestFile.txt`

The script is not meant and must not be run twice, and must be run with a fresh rebasetest branch. 

After a couple of seconds, the script should be done
adding a bunch of trash commits to the branch 'rebasetest'

In your repo, you should be able to use the `git log --oneline --decorate`
command and see the new trash commits, then the final commit that has a sensible 
commit message.

### Setting up master to be one commit ahead.

For a rebase to make any sense, master needs to be at minimum 1 commit ahead.
It is entire possible to create a conflict in this step, but at this point in the tutorial we are not yet going to go into what a conflict is, so we will do the following:

1. Check out the master branch
2. Edit the MyTestFile.txt so it goes from this:

```
Hello World!
And welcome to
the Dominatening!
```

TO

```
# Demo file for rebase tutorial
Hello World!
And welcome to
the Dominatening!
```

3. Save the file, then commit it to master with a sensible message like 'Added a comment to the top of MyTestFile.txt'.

### Bringing it all together and doing the rebase.

Now we have a prepared usecase for learning how to rebase.

```
COMMAND: git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
COMMAND: git log --oneline --decorate
f12ee06 (HEAD -> master) Added a comment to the top of MyTestFile.txt
1c0d0cf (origin/master, origin/HEAD) Update MyTestFile.txt
ae21d86 (mytestbranch) Added a new line of text to file MyTestFile.txt
467c134 Initial commit.
COMMAND: git checkout rebasetest
Switched to branch 'rebasetest'
COMMAND: git log --oneline --decorate
fe49074 (HEAD -> rebasetest) Added a new line to MyTestFile.txt
2e31eff words vs numbers? idk
574e6ca case tweak maybe?
4a8fa2c typo fix? fuck why is it not working
3525a80 initial commit on branch rebasetest
1c0d0cf (origin/master, origin/HEAD) Update MyTestFile.txt
ae21d86 (mytestbranch) Added a new line of text to file MyTestFile.txt
467c134 Initial commit.
```

As we want it to be for this tutorial, the master branch is now 1 commit "ahead" of the commit in the master branch you based the 'rebasetest' branch on.

In a case like this, we want to rebase our rebasetest branch on master, especially
if asked to do so, or before you make the PR.

As (and will be real for you to in real situations) we have a bunch of trash commits that we likely don't want to keep around, we are going to run rebase in interactive mode to 
be able to "squash" the commits.

Run this command in your repo while you have rebasetest branch checked out:

`git rebase -i master`
(The branch you choose is the branch that the currently checked out branch will be rebased onto. It's entirely possible to have a non-master branch that you want to rebase onto, but that's nothing the tutorial will go trough).

You will see this:

```
pick 3525a80 # initial commit on branch rebasetest
pick 4a8fa2c # typo fix? fuck why is it not working
pick 574e6ca # case tweak maybe?
pick 2e31eff # words vs numbers? idk
pick fe49074 # Added a new line to MyTestFile.txt

# Rebase f12ee06..fe49074 onto f12ee06 (5 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

Obviously the hashes will not all be the same.
If on Windows and you picked Notepad as your git editor, git will not continue until 
you save the weird git-rebase-todo file and then close it's tab. It's very important that you do not try to Save As or anything fancy, just Ctrl+S when done editing the file.

On Linux, you will likely have a terminal based editor such as nano or something
as your git editor, in which case git only continues when you
save and then exit the editor.

The examples illustrated will be Windows with Notepad.

We want the first commit you made to this branch to be the pick
and the rest squash, so you end up with this:

```
pick 3525a80 # initial commit on branch rebasetest
squash 4a8fa2c # typo fix? fuck why is it not working
squash 574e6ca # case tweak maybe?
squash 2e31eff # words vs numbers? idk
squash fe49074 # Added a new line to MyTestFile.txt

# Rebase f12ee06..fe49074 onto f12ee06 (5 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

Then Ctrl+S and then close the tab.
Merely a second after (on huge git repos it can take a couple seconds longer)
your editor will again open a new file, this time called 
COMMIT_EDITMSG.

You will see something like this:

```
# This is a combination of 5 commits.
# This is the 1st commit message:

initial commit on branch rebasetest

# This is the commit message #2:

typo fix? fuck why is it not working

# This is the commit message #3:

case tweak maybe?

# This is the commit message #4:

words vs numbers? idk

# This is the commit message #5:

Added a new line to MyTestFile.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Feb 20 21:12:03 2026 +0100
#
# interactive rebase in progress; onto f12ee06
# Last commands done (5 commands done):
#    squash 2e31eff # words vs numbers? idk
#    squash fe49074 # Added a new line to MyTestFile.txt
# No commands remaining.
# You are currently rebasing branch 'rebasetest' on 'f12ee06'.
#
# Changes to be committed:
#	modified:   MyTestFile.txt
#
```

Since it was the final commit we were interested in, we
are going to delete everything so we end up with this:

```
Added a new line to MyTestFile.txt

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Fri Feb 20 21:12:03 2026 +0100
#
# interactive rebase in progress; onto f12ee06
# Last commands done (5 commands done):
#    squash 2e31eff # words vs numbers? idk
#    squash fe49074 # Added a new line to MyTestFile.txt
# No commands remaining.
# You are currently rebasing branch 'rebasetest' on 'f12ee06'.
#
# Changes to be committed:
#	modified:   MyTestFile.txt
#
```

Then Ctrl+S and close the tab.
Unless you have a really good reason to do so, don't keep the old commit messages.

This should be the result in the terminal after you are done (It will be different in Linux):

```
COMMAND: git rebase -i master
hint: Waiting for your editor to close the file... unix2dos: converting file C:/Users/YourUserName/Documents/github-repos/mytestrepo/.git/rebase-merge/git-rebase-todo to DOS format...
dos2unix: converting file C:/Users/CastawayDevTest/Documents/github-repos/mytestrepo/.git/rebase-merge/git-rebase-todo to Unix format...
hint: Waiting for your editor to close the file... unix2dos: converting file C:/Users/YourUserName/Documents/github-repos/mytestrepo/.git/COMMIT_EDITMSG to DOS format...
dos2unix: converting file C:/Users/CastawayDevTest/Documents/github-repos/mytestrepo/.git/COMMIT_EDITMSG to Unix format...
[detached HEAD af91db9] Added a new line to MyTestFile.txt
 Date: Fri Feb 20 21:12:03 2026 +0100
 1 file changed, 2 insertions(+)
Successfully rebased and updated refs/heads/rebasetest.
```

This should be the result now if you look at the logs of your rebasetest branch:

```
COMMAND: git log --oneline --decorate
af91db9 (HEAD -> rebasetest) Added a new line to MyTestFile.txt
f12ee06 (master) Added a comment to the top of MyTestFile.txt
1c0d0cf (origin/master, origin/HEAD) Update MyTestFile.txt
ae21d86 (mytestbranch) Added a new line of text to file MyTestFile.txt
467c134 Initial commit.
```

Notice now how the final commit of our rebasetest branch is above that 1 commit that was ahead in master? This results in a very clean history without distracting "trash" commits.

Now you are ready to merge this into master like you did before:
Check out master, then do `git merge rebasetest`

Then do git status.

You should now see 

```
COMMAND: git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

The reason why it says that you are ahead of master by 2 commits is because
you never pushed the "Added a comment to the top of MyTestFile.txt" commit you made
to master that put it 1 commit ahead of rebasetest. And because we technically created a new commit with this rebase, it results in our local master behind ahead of origin/master by 2.

Go ahead and run the command `git push` to push your updated master
to your github repo.

The text in the textfile both on the github repo's master and your local master should end up being:

```
# Demo file for rebase tutorial
Hello World!
And welcome to
the Dominatening!

Match begins in 10 seconds!
```

With this, you are done with git for now.
If you'd like to read more about git before
we return to git when we start working with the Castaway.tf repo to continue experimenting
on your own, I recommend this book:

https://git-scm.com/book/en/v2

## How to install the TF2 dedicated server.

For this part, I will be linking the wiki tutorials

For Windows, you can simply follow this tutorial:
https://wiki.teamfortress.com/wiki/Windows_dedicated_server

For linux, follow this tutorial:
https://wiki.teamfortress.com/wiki/Linux_dedicated_server

I have some specific comments for linux:
For a basic dev server that you intend to run on your own computer only, you can ignore (if you wish) the following steps from the linux tutorial:

* Adding user
* motd.txt
* mapcycle.txt
* pure_server_whitelist.txt

In the launch script it suggests, set sv_pure to 0 instead of 1,
and add +tv_enable 1 
so you are ready to record with source tv. Source tv will be used to
record demos for you from the perspective of the server, this helps you verify
that other players will see what you intend them to see, let's say if you attach a particle to a player. 
Remove the sv_setsteamaccount thing. That's something you only use if you intend to run a real tf2 server for others.

You can also skip opening the ports and the Utilities and Persistence section.
You might need to use noclip and teleports and a bunch of stuff
while you develop for Castaway.tf, thus it might be prudent to add +sv_cheats 1
to your launch script.

---

Return to this tutorial when you have successfully installed the TF2 dedicated server and launched it once. Also try joining it. It will be on 127.0.0.1 or localhost

Also when you change map on the server, never use the map command.
use the changelevel command, otherwise the server WILL crash.
Oh and do not launch any win64 or linux64 version of srcds.
The reverts do NOT work on 64 bit, and likely
will not for the forseeable future.

## How to install Metamod:Source and Sourcemod

Now with a working TF2 server, you will need to install Metamod:Source
and Sourcemod.

Metamod:Source
https://www.sourcemm.net/downloads.php?branch=stable

1. Click the OS that matches the OS you are on (Either Windows or Linux).
2. Extract the contents of the zip/tar.gz file somewhere.

SourceMod:
https://www.sourcemod.net/downloads.php?branch=stable

1. Click the OS that matches the OS you are on (Either Windows or Linux).
2. Extract the contents of the zip/tar.gz file somewhere.

Now:

1. Combine both addons folders you got from extracting from the two files.
2. Copy this entire combined addons folder and paste it into the `tf` folder of your dedicated server install.
3. Launch the server once to allow Sourcemod to update it's gamedata. Then close the server.

## How to fork and clone the Castaway.tf repo

A **fork** is a personal copy of a Git repository that exists on a server (for example, GitHub).
It allows you to experiment and make commits without having any ability to damage the original repository.

A **clone** is a local copy of a repository on your own computer.
This is where you actually do your work.
Any changes you make locally stay local until you explicitly push them somewhere.

In short:

- **Fork** → your personal copy on GitHub
- **Clone** → your working copy on your computer


## Important rules for Castaway.tf

For Castaway.tf, it is important to understand that the **`master` branch is treated as read-only**.

With the exception of *random*, no one commits directly to `master`.

You should **never create your own commits on `master`** (not locally, not on your fork).
All real development work must happen on feature branches.

Your local `master` is not a work branch.
It exists only as a **clean baseline** that matches the upstream repository when needed.


### Development setup approach used in this tutorial

There are many valid ways to set up a Git development environment.

For this tutorial, we use a setup where you will barely interact with the GitHub website at all,
except when creating pull requests.
Most of the work will be done from the command line.


## Forking and cloning the repository

1. Go to the Castaway.tf repository:
   https://github.com/rsedxcftvgyhbujnkiqwe/castaway-plugins

2. Click the **Fork** button.
3. Make no changes and press **Create fork**.
4. Wait for GitHub to finish creating the fork.
5. Click the green **<> Code** button.
6. Make sure **HTTPS** is selected, then click the copy button.
7. Open a terminal in the `github-repos` folder created earlier in the tutorial.
8. Run:
   `git clone URL`
   where `URL` is the address you copied in step 6.
9. Enter the cloned repository:
   `cd castaway-plugins`


### Adding the upstream (read-only) remote

We want to be able to fetch new commits from the original Castaway.tf repository, but never push to it.

Run the following commands:

git remote add upstream https://github.com/rsedxcftvgyhbujnkiqwe/castaway-plugins.git
git remote set-url --push upstream no_push

This results in:
- `origin` → your fork (fetch + push)
- `upstream` → original repository (fetch only)

Trying to push to `upstream` will now fail immediately.


### Updating your local master baseline

Your local `master` is a **baseline**, not a work branch.
Updating it does not create commits; it only moves your `master` pointer to commits that already exist upstream.

To update your local `master` so it matches the current upstream state, run:

git fetch upstream
git checkout master
git reset --hard upstream/master

The final command discards any local commits on `master`
and moves it's commit pointer to reflect what the original repo master is.

In some other projects this would be dangerous (it all depends on the workflow the team/maintainer is using)
For Castaway.tf, this is intentional, because `master` is never used for development.
If there were local commits on the `master` branch that do not exist upstream, they are
likely commits you have accidentally merged into master.


### Updating your fork’s master baseline

Your fork (`origin`) also has a `master` branch.
After updating your local `master`, you should update your fork’s `master` to reflect the same upstream state.

Update your fork like this:

`git push origin master --force-with-lease`

Summary:
- You never add your own commits to `master`.
- `master` is a clean baseline, updated only when needed.
- All real work happens on feature branches.

One more thing: While I did mention that it's good to rebase
onto latest master, this is not always neccesary, once you have uploaded your branch
to your origin, you should try opening a pull request. Github will tell you if it can be cleanly merged or not. If it can be cleanly merged and you are done
with working on the feature branch, then feel free to create the pull request even tough you have not rebased on latest master. But if it cannot be cleanly merged, then you MUST rebase onto latest master, cancel the creation process of the pull request, rebase onto the latest castaway.tf master, then open a new pull request and check again.

## Installing the dependencies to run the reverts.sp plugin and adding dependencies to compile it.

You are going to need to fullfill the dependencies that the reverts plugin has
in order to run it on the server, and to compile it.

This is when you will need to decide if you are going to
go old-school-ish with a editor (anything from Notepad to Sublime etc)
or a full IDE. The obvious benefit with using a IDE
is that you get things like autocompletion etc and other stuff that makes life easier.

But first, let's gather up the dependencies you need.


## Dependencies to run the reverts.sp plugin
I've gone ahead and created scripts to help you with this.

Pick the appropiate script for your os.
Paste it into your text editor and create them 
as `fetch-revert-deps.sh` for linux.
or `fetch-revert-deps.ps1` for windows.

Command to run it on Windows:
`powershell -ExecutionPolicy Bypass -File .\fecth-revert-deps.ps1`

Linux users can make do with a simple `./fetch-revert-deps.sh`, make sure you give the file permission to run as script

The script will prompt you at the end if you want to delete the .tmp (Linux)
or tmp (Windows) folder. Check the path so you are not deleting something else on the computer, answer y when ready.

a `linux` or `windows` folder will be created in the same folder where you placed the script file
and ran it from. Copy the addons folder to your tf folder on your dedicated TF2 server.

**Linux:**

```
#!/bin/sh
set -eu

# ----- OS GUARD -----
if [ "$(uname -s)" != "Linux" ]; then
    echo "ERROR: This script must be run on Linux." >&2
    exit 1
fi

TMPDIR=".tmp"
TMP_ABS="$(cd "$(dirname "$TMPDIR")" && pwd)/$TMPDIR"

cleanup() {
    echo
    echo "Temporary files were extracted to:"
    echo "  $TMP_ABS"
    echo
    printf "Delete temporary files from extraction phase? Check path first! [y/N]: "
    read ans || true

    case "$ans" in
        y|Y)
            echo "Deleting temporary files..."
            cd .. || exit 1
            rm -rf "$TMPDIR"
            ;;
        *)
            echo "Keeping temporary files."
            ;;
    esac
}

trap cleanup EXIT

# ----- SETUP -----
mkdir -p \
  linux/addons/sourcemod/{extensions,gamedata,plugins,translations} \
  "$TMPDIR"

cd "$TMPDIR"

# ================= TF2Items =================
curl -LO https://builds.limetech.io/files/tf2items-1.6.4-hg279-linux.zip
unzip -q tf2items-1.6.4-hg279-linux.zip -d tf2items-linux

cp tf2items-linux/addons/sourcemod/extensions/tf2items.ext.2.ep2v.so \
   ../linux/addons/sourcemod/extensions/
cp tf2items-linux/addons/sourcemod/extensions/tf2items.autoload \
   ../linux/addons/sourcemod/extensions/
cp tf2items-linux/addons/sourcemod/gamedata/tf2.items.txt \
   ../linux/addons/sourcemod/gamedata/

# ================= TF2Attributes =================
base=https://github.com/FlaminSarge/tf2attributes/releases/download/v1.7.5

curl -LO $base/tf2.attributes.txt
curl -LO $base/tf2attributes.smx

cp tf2.attributes.txt ../linux/addons/sourcemod/gamedata/
cp tf2attributes.smx  ../linux/addons/sourcemod/plugins/

# ================= TF2Utils =================
base=https://github.com/nosoop/SM-TFUtils/releases/download/1.4.0

curl -LO $base/tf2.utils.nosoop.txt
curl -LO $base/tf2utils.smx

cp tf2.utils.nosoop.txt ../linux/addons/sourcemod/gamedata/
cp tf2utils.smx         ../linux/addons/sourcemod/plugins/

# ================= SourceScramble =================
curl -LO https://github.com/nosoop/SMExt-SourceScramble/releases/download/0.7.1/package.tar.gz
tar -xzf package.tar.gz

if [ ! -f addons/sourcemod/extensions/sourcescramble.ext.so ]; then
    echo "ERROR: sourcescramble.ext.so not found after extraction." >&2
    exit 1
fi

cp addons/sourcemod/extensions/sourcescramble.ext.so \
   ../linux/addons/sourcemod/extensions/

# ================= nativevotes =================
curl -LO https://github.com/sapphonie/sourcemod-nativevotes-updated/archive/refs/heads/master.zip
unzip -q master.zip

cp -r sourcemod-nativevotes-updated-*/addons/sourcemod/translations \
      ../linux/addons/sourcemod/

echo
echo "Linux dependencies installed."

# ================= README =================
cat > ../linux/README.txt <<'EOF'
addons folder contains dependencies needed to run the reverts.sp plugin.
copy the addons folder and paste it into the tf folder of your TF2 dedicated server
EOF

echo "Generated linux/README.txt"
```

**Windows:**

```
$ErrorActionPreference = "Stop"

if ($env:OS -ne 'Windows_NT') {
    Write-Error "This script must be run on Windows."
    exit 1
}

function New-Dirs {
    param ($Base)
    $paths = @(
        "$Base/addons/sourcemod/extensions",
        "$Base/addons/sourcemod/gamedata",
        "$Base/addons/sourcemod/plugins",
        "$Base/addons/sourcemod/translations"
    )
    foreach ($p in $paths) {
        New-Item -ItemType Directory -Force -Path $p | Out-Null
    }
}

function Download {
    param ($Url, $Out)
    Write-Host "Downloading $Url"
    Invoke-WebRequest -Uri $Url -OutFile $Out
}

# ----- SETUP -----
New-Dirs "windows"
$temp = "tmp"

try {
    New-Item -ItemType Directory -Force -Path $temp | Out-Null

    # ================= TF2Items (Windows) =================
    Download "https://builds.limetech.io/files/tf2items-1.6.4-hg279-windows.zip" `
             "$temp/tf2items-win.zip"

    Expand-Archive "$temp/tf2items-win.zip" "$temp/tf2items-win"

    Copy-Item "$temp/tf2items-win/addons/sourcemod/extensions/tf2items.ext.2.ep2v.dll" `
              "windows/addons/sourcemod/extensions/"
    Copy-Item "$temp/tf2items-win/addons/sourcemod/extensions/tf2items.autoload" `
              "windows/addons/sourcemod/extensions/"
    Copy-Item "$temp/tf2items-win/addons/sourcemod/gamedata/tf2.items.txt" `
              "windows/addons/sourcemod/gamedata/"

    # ================= TF2Attributes =================
    $attrBase = "https://github.com/FlaminSarge/tf2attributes/releases/download/v1.7.5"

    Download "$attrBase/tf2.attributes.txt" "$temp/tf2.attributes.txt"
    Download "$attrBase/tf2attributes.smx"  "$temp/tf2attributes.smx"

    Copy-Item "$temp/tf2.attributes.txt" "windows/addons/sourcemod/gamedata/"
    Copy-Item "$temp/tf2attributes.smx"  "windows/addons/sourcemod/plugins/"

    # ================= TF2Utils =================
    $utilsBase = "https://github.com/nosoop/SM-TFUtils/releases/download/1.4.0"

    Download "$utilsBase/tf2.utils.nosoop.txt" "$temp/tf2.utils.nosoop.txt"
    Download "$utilsBase/tf2utils.smx"         "$temp/tf2utils.smx"

    Copy-Item "$temp/tf2.utils.nosoop.txt" "windows/addons/sourcemod/gamedata/"
    Copy-Item "$temp/tf2utils.smx"         "windows/addons/sourcemod/plugins/"

    # ================= SourceScramble (Windows) =================
    Download "https://github.com/nosoop/SMExt-SourceScramble/releases/download/0.7.1/package.zip" `
             "$temp/sourcescramble.zip"

    Expand-Archive "$temp/sourcescramble.zip" "$temp"

    $scrambleDll = Join-Path $temp "addons\sourcemod\extensions\sourcescramble.ext.dll"

    if (-not (Test-Path $scrambleDll)) {
        throw "sourcescramble.ext.dll not found after extraction."
    }

    Copy-Item $scrambleDll "windows/addons/sourcemod/extensions/"

    # ================= nativevotes =================
    Download "https://github.com/sapphonie/sourcemod-nativevotes-updated/archive/refs/heads/master.zip" `
             "$temp/nativevotes.zip"

    Expand-Archive "$temp/nativevotes.zip" "$temp/nativevotes"

    $translations = Get-ChildItem "$temp/nativevotes" -Recurse -Directory |
                    Where-Object { $_.Name -eq "translations" } |
                    Select-Object -First 1

    if (-not $translations) {
        throw "nativevotes translations folder not found."
    }

    Copy-Item $translations.FullName "windows/addons/sourcemod/" -Recurse -Force

    Write-Host ""
    Write-Host "Windows dependencies installed."

    # ================= README =================
    @"
addons folder contains dependencies needed to run the reverts.sp plugin.
copy the addons folder and paste it into the tf folder of your TF2 dedicated server
"@ | Set-Content "windows/README.txt"

    Write-Host "Generated windows/README.txt"
}
finally {
    Write-Host ""
    Write-Host "Temporary files were extracted to:"
    Write-Host "  $(Resolve-Path $temp)"
    Write-Host ""
    $ans = Read-Host "Delete temporary files from extraction phase? Check path first! [y/N]"
    if ($ans -match '^[yY]$') {
        Remove-Item -Recurse -Force $temp
        Write-Host "Temporary files deleted."
    } else {
        Write-Host "Keeping temporary files."
    }
}
```

When the script is done, you will see a windows or linux folder, inside
of it you will see a README.txt, read it for further instructions.

## Dependencies to compile the reverts plugin.

The Castaway.tf repo fork (and local clone of it, aka the `castaway-plugins` folder) that you have,
contains everything you need. 
The only thing you need to do, is to copy the

`include` folder
and the spcomp file (on Windows it will have a .exe) from
`tf/addons/sourcemod/scripting` folder into your castaway-plugins/scripting folder

This is what you want the structure to look like this for the `scripting` folder
(the . represents `castaway-plugins/scripting`):

```
.
├── afkmanager.sp
├── arena-autoscramble.sp
├── changelevel.sp
├── chat-adverts.sp
├── disablesoul.sp
├── forcestalemate.sp
├── include
│   ├── admin.inc
│   ├── adminmenu.inc
│   ├── adt_array.inc
│   ├── adt.inc
│   ├── adt_stack.inc
│   ├── adt_trie.inc
│   ├── banning.inc
│   ├── basecomm.inc
│   ├── bitbuffer.inc
│   ├── clientprefs.inc
│   ├── clients.inc
│   ├── commandfilters.inc
│   ├── commandline.inc
│   ├── console.inc
│   ├── convars.inc
│   ├── core.inc
│   ├── cstrike.inc
│   ├── datapack.inc
│   ├── dbi.inc
│   ├── dhooks.inc
│   ├── entity.inc
│   ├── entitylump.inc
│   ├── entity_prop_stocks.inc
│   ├── events.inc
│   ├── files.inc
│   ├── float.inc
│   ├── functions.inc
│   ├── geoip.inc
│   ├── halflife.inc
│   ├── handles.inc
│   ├── helpers.inc
│   ├── implodeexplode.inc
│   ├── keyvalues.inc
│   ├── lang.inc
│   ├── logging.inc
│   ├── mapchooser.inc
│   ├── menus.inc
│   ├── morecolors.inc
│   ├── nativevotes.inc
│   ├── nextmap.inc
│   ├── profiler.inc
│   ├── protobuf.inc
│   ├── regex.inc
│   ├── scramble.inc
│   ├── sdkhooks.inc
│   ├── sdktools_client.inc
│   ├── sdktools_engine.inc
│   ├── sdktools_entinput.inc
│   ├── sdktools_entoutput.inc
│   ├── sdktools_functions.inc
│   ├── sdktools_gamerules.inc
│   ├── sdktools_hooks.inc
│   ├── sdktools.inc
│   ├── sdktools_sound.inc
│   ├── sdktools_stocks.inc
│   ├── sdktools_stringtables.inc
│   ├── sdktools_tempents.inc
│   ├── sdktools_tempents_stocks.inc
│   ├── sdktools_trace.inc
│   ├── sdktools_variant_t.inc
│   ├── sdktools_voice.inc
│   ├── sorting.inc
│   ├── sourcemod.inc
│   ├── sourcescramble.inc
│   ├── string.inc
│   ├── testing.inc
│   ├── textparse.inc
│   ├── tf2attributes.inc
│   ├── tf2condhooks.inc
│   ├── tf2.inc
│   ├── tf2items.inc
│   ├── tf2_stocks.inc
│   ├── tf2utils.inc
│   ├── timers.inc
│   ├── topmenus.inc
│   ├── usermessages.inc
│   ├── vector.inc
│   ├── version_auto.inc
│   └── version.inc
├── legacy
│   ├── NotnHeavy - Old Flamethrower Mechanics.sp
│   └── NotnHeavy - Pre-Gun Mettle Reverts.sp
├── nativevotes
│   ├── data-keyvalues.sp
│   └── game.sp
├── nativevotes-basecommands.sp
├── nativevotes_mapchooser.sp
├── nativevotes_nominations.sp
├── nativevotes_rockthevote.sp
├── nativevotes.sp
├── nextmap.sp
├── reverts.sp
├── spcomp
├── supersprayhandler.sp
├── teamcatch.sp
├── tf2condhooks.sp
├── votescramble.sp
└── webshortcuts.sp
```

You may or may not see the names in different orders. The important thing is that the files are there. If a file is not there or you see some other name after setup, then
castaway or sourcemod might have added or removed .sp files. The state that I showed you was true as of 2026-02-24.

## Compiling reverts.sp

99% of the work you will do on the Castaway.tf repo will be about the reverts plugin in some form or another.

Compiling the plugin is as easy as 
running one of the following commands depending on what OS you are using
(Open a terminal at `castaway-plugins/scripting`):

**Linux:** `./spcomp reverts.sp`
**Windows:** `./spcomp.exe reverts.sp`

When you run it without arguments, the Linux version will be compiled.
If you want to compile the Windows version, you need to add `=WIN32` like this:

**Linux:** `./spcomp reverts.sp WIN32=`
**Windows:** `./spcomp.exe reverts.sp WIN32=`

### Why are they seperated? I thought SourceMod is generally programmed to be OS agnostic?

Because of the memorypatches. The architecture is different between Linux and Windows
when it comes to how memory is laid out when the TF2 Dedicated server is compiled by Valve. Thanks to tools like SourceScramble, we can cut down on alot of SourcePawn (The language of SourceMod) specific coding, however some memorypatch reverts absolutely depend
on us making seperate compiles of the reverts.sp, and thus it is the way it is.

SourcePawn does a poor job of allowing us to properly check which OS we are on in script.
Because of this, we need the one compiling (such as yourself) to manually tell us which OS
we are supposed to run the plugin in.

IF a better solution is found someday, then we might use that. But until then this is how it has to be.

### Patchless (aka no memorypatches)

The plugin has a option for compiling it without memorypatches.
Use this:

`NO_MEMPATCHES=`

Like this:

**Linux:** `./spcomp reverts.sp NO_MEMPATCHES=`
**Windows:** `./spcomp.exe reverts.sp NO_MEMPATCHES=`

(You do not and should not try to define WIN32= if intend to compile patchless).

Short QA:

Q: I got an error
A: Read the error then either search for it on the internet (do this first!) or
ask one of us who work on the plugin. 

### After compilation

In the same folder as the spcomp, you will now see a `reverts.smx`
file (it matches the name of the script you compiled).

Copy this file and place it at `tf/addons/sourcemod/plugins`
then go ahead and run your server. 

Observe if you see any errors and read further on the wiki of the Castaway.tf 
github repo for more help.

## Overview of the Castaway.tf work progress.

The general way you want to work with the repo is the following (this is based on my own workflow):

1. Identify something you think you can improve or add. Or ask the other devs, or look at the issues page of the Castaway.tf github repo for something to work on, or just ask a Castaway.tf player.
2. Open 3 terminals. One at `castaway-plugins`, `castaway-plugins/scripting` and the folder of your dedicated TF2 server. The first will be used for git commands, the second will be used for compiling the reverts plugin, the third will be used to launch the server.
3. Do research on what you want to add or improve. Is a weapon unreverted? Read the TF2 wiki, watch old youtube videos of the weapon being used at the time you are interested in etc. Figured out a better way to optimize the code?
4. In the terminal you will run git commands at, make sure you are on master, then check out a new branch based on `master` with a appropiate pre-fix and name. For example let's say you are adding a new revert for the Gunboats, then maybe `revert/gunboats-pre-jan-2010` could be appropiate. Is it a optimization? Then maybe
`optimize/gunboat-damage-calc`. Is it a fix for a issue? Perhaps `issue-xxx/fixed-sound-spam`
5. Get to coding.
6. Compile, test your compile on your local TF2 server (unless it's a memorypatch or complicated math, you really don't need to ask for help with testing on the opposite OS in the PR).
7. Keep repeating steps 5 and 6. Making sure you remember to commit so you don't do to much work in each commit. Don't forget to occasionally push to your castaway.tf repo fork either. You absolutely want to be doing this if you need to ask the rest of us for help instead of sending pastebins and shit.
8. Once whatever you wanted to do works and you have tested it in as many ways as you can imagine (and bother to do, LOL), make a git tag (more on that later) backup.
9. Push it a final time to your fork, then go make a PR to the Castaway.tf repo and observe if it says it can be cleanly merged or not.

If it can be cleanly merged, open the PR, don't forget to fill out the template and describe what you have done before you open the PR.

It it CANNOT be cleanly merged, rebase on latest master.
10. Wait for feedback from others or any requests from random.
(Depending on how busy random is and how complex the PR is, it can take anywhere from a day to several days before it's merged).

If others find bugs, repeat steps 5 and 6 until it's fixed.
Make sure these commits are sensible and not the typical trash commit messages.
Also, DO NOT OPEN A NEW PR! The PR you opened earlier will autoupdate with the latest commits each time you push to your fork (origin), as the PR tracks what happens to your origin branch.

