# Working with Git and Github

Just the commands

## Git configuration
```zsh
$ git config --global user.name "Your Name"
$ git config --global user.email your-email@example.com
$ git config --global core.editor "code --wait"
```

Set how lin endings should be handled depending on system:
```zsh
# Windows:
> git config --global core.autocrlf true
# Mac/Linux:
$ git config --global core.autocrlf input
```

View global git config
```zsh
$ git config --global -e
```

## Set up a Git project to use with Github

```zsh
$ echo "# My new repository" >> README.md
$ git init
$ git add .
$ git commit -m "Initial commit"
$ git branch -M main
# Create empty repository on Github before the next command
$ git remote add origin git@github.com:<username>/<repository>.git
$ git push -u origin main
```
Check status, add files, commit and push changes:
```zsh
$ git status
$ git add .
$ git commit
$ git push
```


## Create and clone from Github

```zsh
$ git clone git@github.com:<username>/<repository>.git
$ git clone git@github.com:<username>/<repository>.git <new-folder-name>
```

## Set up SSH keys and add them to your account

```zsh
$ ssh-keygen -t ed25519 -C "your_name@example.com"
eval `ssh-agent -s`
ssh-add ~/.ssh/id_ed25519
```

## Working with branches

```zsh
$ git branch <new-branch-name>
$ git branch -a
$ git checkout <new-branch-name>
# Either
$ git push origin <new-branch-name>
$ git branch --set-upstream-to=origin/<new-branch-name> <new-branch-name>
# or
$ git push --set-upstream origin <new-branch-name>
```
