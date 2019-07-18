---
layout: default
title: "Version Control"
parent: "Team Reference"
permalink: /docs/reference/vcs
---

# Version Control for 5024

## GitKracken
GitKraken is a GUI that streamlines the Git workflow. It doesn’t require Git Bash but you should have that installed on your computer anyway. To use GitKraken, download it from [GitKracken.com](https://www.gitkraken.com/). When it has finished installation, log in with your GitHub Account.

However, before you use the application, you should learn your way around the interface. This can be done by reading the [GitKracken quick-start Guide](https://support.gitkraken.com/start-here/guide). 

## Learning the Basics
These are the basic actions that every programmer must know in order to use GitKracken:

 - [Clone a Repo](https://support.gitkraken.com/working-with-repositories/open-clone-init#cloning-an-existing-project)
 - [Make a Branch](https://support.gitkraken.com/working-with-repositories/branching-and-merging#branches)
 - [Stage, Commit, and Push Code](https://support.gitkraken.com/working-with-repositories/pushing-and-pulling)
  
The GitKracken team has also provided a great guide for learning Git. It is avalible at the link below: <br>
https://support.gitkraken.com/start-here/guide


## Using the Command Line Interface
Git Bash is the Windows command-line version of Git. It works exactly the same as regular Git, but instead of using cmd, the stock windows terminal, commands are entered into the Git Bash terminal. Git Bash can be downloaded from the [Git website](https://git-scm.com/download/win).

Git has many commands for it's various tasks. The commands most used by out team are the following:
```
git clone https://example.com/project.git
git add .
git commit -m “This is a commit message"
git push
git checkout branch-name
```

A very useful cheat-sheet is avalible on the [git-tower](https://www.git-tower.com/blog/content/posts/54-git-cheat-sheet/git-cheat-sheet-large01.png) website.

## Proper Branch Usage
Before you make a new branch, make sure you have the newest code on your computer. To do this, run the `git pull` command or press the **pull** button in GitKraken.

Never push to the master branch without a code review. The master branch should always contain fully operation and review code that has been approved by a mentor, unless a mentor specifically asks you to push some non-reviewed code.

Do NOT do work in the master branch on your computer. If you need to change code, do it in a separate branch. THis makes it easier if you need to copy your code to another computer and will make sure that you don't get errors while pushing code.

When pushing code to the robot, always push the master branch, unless you are testing something on your own branch. At the end of the day / meeting, make sure the robot has the newest code from master pushed to it in case another subteam needs to use the robot.
