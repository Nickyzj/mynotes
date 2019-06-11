# Git

[Git Tutorial for Beginners: Command-Line Fundamentals](<https://www.youtube.com/watch?v=HVsySz-h9r4&t=1119s>)

Distributed Version Control System

```shell
git --version

git config --global user.name <name>
git config --global user.email <email>

git config --list

git help <verb>
git <verb> --help

git init # Create .git folder

git status

touch .gitignore

git add -A # Add all files to staging area

git reset # Remove files from staging area

git commit -m "Initial Commit"

git log

git clone <url> <where to clone>

# Viewing information about the remote repo
git remote -v
git brance -a

git diff # Show changes

git pull origin master
git push origin master
```

![1560219102064](<https://raw.githubusercontent.com/Nickyzj/mynotes/master/resume/images/1560219102064.png>)



## Common Workflow

```shell
# Create a branch for desired feature

git branch calc-divide # Create branch
git branch # List all branches

git checkout calc-divide # Switch to branch
# After commit no affect to master branch or remote repo

# After commit
# Push branch to remote
git push -u origin calc-divide

git branch -a # Show both local branches and remote branches

# Merge a branch
git checkout master

git pull origin master # Make sure download latest version

git branch --merged 

git merge calc-divide

git push origin master

# Delete a branch
git branch -- merged
git branch -d calc-divide # Delete branch locally
git branch -a
git push origin --delete calc-divide
```



##  Faster example

```shell
git branch subtract
git checkout subtract
git status
git add -A
git commit -m "subtract"
git push -u origin subtract

git checkout master
git pull origin master
git merge subtract
git push origin master
```

