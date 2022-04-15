# Working with Git and Github

My own notes for setting up Git and using it with Github.

## Download git
For Mac and windows, download Git from here: https://git-scm.com/downloads
For Windows, if you want to do any kind of scripting in Git bash select to install all unix tools, otherwise accept the default values.

For Linux, use a suitable package manager for your system. Example:
```zsh
$ sudo apt install git
```

## Git configuration
In a terminal, set up name and email so people know who made the changes:
```zsh
$ git config --global user.name "Your Name"
$ git config --global user.email your-email@example.com
```
Next set up VS Code as the editor for Git commit messages and have Git wait until the commit message file is closed before continuing. The command "code" must be in your path and start VS Code for this to work. This should work by default on Windows and Linux. To add "code" to path on Mac, see documentation here: https://code.visualstudio.com/docs/setup/mac. In short:
```zsh
1. Open VS Code
2. Press ctrl+shift+p to open the command palette
3. Type "shell command" in the search
4. Select "Shell Command: Install 'code' command in PATH"
5. Restart your terminal
```
Then execute this command in the terminal to use VS Code by default:
```zsh
$ git config --global core.editor "code --wait"
```

Lastly, set up how line endings should be handled to avoid problems when cooperating with people using a different system. Windows uses CR LF for line endrings, Linux/Mac only uses LF. So if you are on Windows CR should be removed when pushing code to the repository, and added when you are pulling code from it. For Linux and Mac, line endings should not be touched when pulling code from the repository, but in case the editor used has added CR, remove it when pushing to the repository.

On Windows:
```zsh
> git config --global core.autocrlf true
```

Mac/Linux:
```zsh
$ git config --global core.autocrlf input
```

To view your git config:
```zsh
$ git config --global -e
```

## Set up a Git project to use with Github

There are two ways to start a new project and use it with Github. Either initialize it locally first and then connect it to GitHub, or create it on Github first and clone it to get a local copy. If you create a new, empty repository on Github, there will be instructions on how to connect to it. If readme, gitignore or license files are added, no instructions are shown.

## Initialize locally

In a directory of your choosing, create the files you want to add to Github. At the very minimum create a readme file. From the commandline in a terminal:

```zsh
$ echo "# My new repository" >> README.md
$ git init
$ git add .
$ git commit -m "Initial commit"
```

Create a new, empty repository on Github and note the address to it.
It will have a format like this: ```git@github.com:<username>/<repository>.git```

Then add remote address to repository and push what we've got so far:
```zsh
$ git branch -M main
$ git remote add origin git@github.com:<username>/<repository>.git
$ git push -u origin main
```
When changes has been made, check the status of your repository:
```zsh
$ git status
```
Files that are updated will have to be added and pushed.
```zsh
$ git add .
```
Commit and then then push the changes to Github:
```zsh
$ git commit
$ git push
```


## Create and clone from Github

If you create a repository on github.com and initialize it with some files, like the readme, gitignore or license, the easiest way to get a local copy to work with is git clone. This will create a folder with the repository name:
```zsh
$ git clone git@github.com:<username>/<repository>.git
```

If for some reason you want the local folder to be called something other than the repository name, that can be added as a parameter:
```zsh
$ git clone git@github.com:<username>/<repository>.git <new-folder-name>
```
A cloned repository like this has already been initialized so the ```git init``` command is not needed when working with it.

## Set up SSH keys and add them to your account

If you don't have a suitable SSH key already, create one first:
```zsh
$ ssh-keygen -t ed25519 -C "your_name@example.com"
```
The -C parameter lets you add a comment to the key, and here we set it to an email address but it can be anything. If not set it will be something like "username@DESKTOP-E7B5H2C" depending on your system
Accept the default name for the key and set a strong password for it.

Start the ssh-agent which will remember your password, so you don't have to type it every time you use SSH:
```zsh
eval `ssh-agent -s`
```
Next add your key and password to ssh-agent:
```zsh
ssh-add ~/.ssh/id_ed25519
```
Note that ssh-agent has to be restarted after each reboot and the key with password has to be added every time ssh-agent is started

Finally, copy the contents of the ```id_ed25519.pub``` file and add it to Github. If you see ```-----BEGIN OPENSSH PRIVATE KEY-----``` in the file, it's the wrong one, that one should be kept private.
In Github, SSH keys are found under profile and then "SSH and GPG keys" in the menu on the left. Click "New SSH Key", give it a title, and add they key in the "key" input field.

## Working with branches

Create a new branch locally from the point you are at now. Basically take a copy of current status:
```zsh
$ git branch <new-branch-name>
```

List all available branches:
```zsh
$ git branch -a
```

Switch to the new branch to make changes to it:
```zsh
$ git checkout <new-branch-name>
```

After changes have been added and committed, push them to Github:
```zsh
$ git push origin <new-branch-name>
```

Now the local changes are stored on Github, but there is no "connection" between the local branch and Github so it can't easily be pulled down again. To set tracking information so they are connected:
```zsh
$ git branch --set-upstream-to=origin/<new-branch-name> <new-branch-name>
```
Now this new branch can be modified and changes pushed as easily as for main.

Going ```git push``` on a local branch before tracking information is set gives an error message, and possibly the command to achieve the last two commands above in one go, but I haven't tried it yet:
```zsh
$ git push --set-upstream origin <new-branch-name>
```
