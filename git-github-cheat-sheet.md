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
Todo

## Set up SSH keys and add them to your account
Todo
