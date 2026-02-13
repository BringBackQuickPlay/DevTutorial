# Guide for setting up a dev enviroment to become credit to team.

Have you ever wondered what you could do to contribute to Castaway.tf?
One thing you could do, is become familiar with the coding (more like scripting really, but who gives a fuck? Normies certainly don't) aspect of Castaway.tf

Bold You too can become a keyboard slave! End Bold. Screaming into the night at compilation errors and help rectify the mistake that is Post-2013 Valve.

This tutorial will teach you several things (the basics mind you)
for getting setup.

* How to create a Github account
* How to install Git
* Setting up SSH key and testing connection to Github (Linux)
* The basics of navigating in a terminal
* Creating a repository (aka 'repo') in git.
* Making a branch in git.
* Comitting, pushing, merge in git.
* How to install the TF2 dedicated server.
* How to install Metamod:Source and Sourcemod
* How to fork the Castaway.tf repo
* How to work with Sourcemod


After all that, we will go trough some additional things
that are more specific to Castaway.tf's repo, such as
general dev conventions.

For learning sourcemod itself, you will have to go find a tutorial online, or be a lazy bastard like me and vibecode half the things and learn "as you go".


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
There's the case with setting from github's retarded DEI "main" to "master" as the default branch, but I personally never got it working.
You can try fixing their gay shit by going to 'Repositories' under the section 'Code, planning, and automation' and changing it in the box at the top.

## How to install git

In order to be able to contribute to the castaway.tf repo, you will need a software called git.
It was written by a very cool nerd from Finland (Perkele) called Linus Torvalds for version control for the Linux Kernel. He's pretty based all things considered since he only cares about merits and hates retards.

It has proven invalueable to basement dwelling nerds for many years now, and it will be of use to you too.

At this point, the tutorial will split up into Windows
and Linux specific points, and they will merge and diverge as needed.
The tutorial assumes that people on Linux are more capable of less handholding as there's already plenty of tutorials and examples online.
Windows users typically need a bit more handholding.

### Linux
Git is almost always already installed with your choosen distro already, if it's not, you will need to go lookup the specific instructions on installing it for your choosen distro.

### Windows

Windows have a fairly easy time getting setup with git.
Begin by visiting this link:
https://git-scm.com/install/windows

You want Windows/X64
Run the installer, and click next on everything besides two things:

When the installer asks you about what editor to use for git, I suggest
notepad. Every Windows user has Notepad. You can ofc choose something else
but this tutorial will not focus on that. What it means is that
when you for example need to resolve a conflict in git (more on that later), git will open your chosen editor to do stuff in.

Another thing the installer will ask you about is the default branch name,
You want to select the option that allows you to set your own, and ensure it says "master" (without the "").

When you are done with the install, open the Windows Start Menu and start typing 'Powershell'. Start Powershell.

Type the following command into the terminal:
`git --version`

You should get a positive reply with the version of git.

(For Linux), we want to ensure you don't get 
infected with the DEI mindvirus whenever Git 3.0 comes out in the future, run this command in a terminal:

`git config --global init.defaultBranch master`
This sets the default branchname to master, which is what proper people will have for their repositories. Only a faggot would willingly let insane trannies dictate to them what and how their tech is to be used (I'm not joking, that faggot who tried to implement the CoC (Code of Conduct) onto Linux and places like Github is a literal insane tranny.

Being proper people, we will not allow that bullshit.

The next section 'Setting up SSH key and testing connection to Github (Linux)' is specifically for Linux, Windows peeps can skip to 'The basics of navigating in a terminal', as we will deal with the setup of authentication for Windows users in the "Pushing" part of the 'Comitting, pushing, merge in git'.

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

7. You will be asked for the passphrase you used (if you set one). This only needs to be entered once per terminal window/session you run step 5 and 6 in. There are ways to make it less painful, but I won't go trough it in this tutorial.

8. Go to the .ssh folder of your user, find the keyname.pub you created, open it with your preffered editor. Copy all the text inside of it. Make damn well sure you are not copying from the keyname file, it MUST be the one file that ends in .pub
!!!
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
1. Start by using the `cd` command to move into your user folder.

2. When there, make a folder named 'castaway', we will be using this folder for the rest of the tutorial.

3. cd into that folder and create these two folders: 'tf2-server' and 'repos'

4. cd into the 'repos' folder.

5. make a folder named 'mytestrepo' and cd into it.

Unless you are told otherwise, It's assumed you work in the same terminal always and that your current working directory is:

Windows:
Linux: `/home/yourusername/castaway/repos/mytestrepo`

### Initializing a git repo.

While in the mytestrepo folder, run this command: `git init`.
This will create a git repository inside of your folder.

Now follow along:

Using your favorite text editor (Notepad is fine for these basic tasks), create
a file named 'MyTestFile.txt'.

Remember how I told you that normally you should avoid BIG LETTERS to make it easier for Linux? This is not a iron clad rule depending on the kind of programming that's being done, especially not for files. I did say to try to avoid it. In our specific example,
we are essentially using CamelCase.

Enter the following into the text file:

`Hello World`.

Save the file as a normal .txt file.

Now in your terminal, type `git status`.
You will see the following (the pre-amble you typically see in a terminal has been removed leaving only the command since it's OS agnostic)

```
git status
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
git add MyTestFile.txt
git status
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

`git config user.name ""`
Set the name that will be displayed on the commit. Here you want to set it to the same you have on Github, if you did not set a specific name in the Profile in Settings on Github, use the github account name. You can technically use whatever you want here, but please be consistent.

With these things done, you are now ready to commit your staged changes:

`git commit -m "Initial commit."`

This will create a commit (a 'snapshot' if you want to use another name for it. But formally it's called a commit and it's what the tutorial will use) of the state of all the tracked files at that particular point in time. 

