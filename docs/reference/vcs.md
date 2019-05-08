# Version Control System for 5024

## GitKracken
GitKraken is a GUI that streamlines using Git. It doesn’t require Git Bash but you should have that installed on your computer anyway. To use GitKraken, download it from https://www.gitkraken.com/. When it has finished installing, you have to log in with your GitHub Account.

Before you do anything however, you should Learn the tool your working with by Learning the Interface. Which can be done at: https://support.gitkraken.com/start-here/guide. 

## Learning the Basics
These are the basic actions the every programmer must know how to do in GitKracken:

 - [Clone a Repo](https://support.gitkraken.com/working-with-repositories/open-clone-init#cloning-an-existing-project)
 - [Make a Branch](https://support.gitkraken.com/working-with-repositories/branching-and-merging#branches)
 - [Stage, Commit, and Push Code](https://support.gitkraken.com/working-with-repositories/pushing-and-pulling)
  
The GitKracken team has also provided this great guide for learning Git: <br>
https://support.gitkraken.com/start-here/guide


## Using the Command Line Interface
Git Bash is the Windows version of Git. It works exactly the same, but instead of using the terminal, commands are entered into the Git Bash program. It can be downloaded from here: https://git-scm.com/download/win.

Git has many commands to do various tasks. The ones most used by us are:
```
git clone https://website.here/project.git
git add
git commit -m “This is a commit message
git push
git checkout branch-name
```
A list of other commands can be found here: <br>
https://www.git-tower.com/blog/content/posts/54-git-cheat-sheet/git-cheat-sheet-large01.png.

## Branch Proper Usage
Before you make a new branch, make sure you have the newest code on your computer. To do this, run the git pull command or by pressing the pull button in GitKraken.

Never push to the master branch without a code review. The master branch should always contain fully operation and review code that has been approved by a mentor, unless a mentor specifically asks you to push some non-reviewed code.

Do NOT do work in the master branch on your computer. If you need to change code, do it in a separate branch. THis makes it easier if you need to copy your code to another computer and will make sure that you don't get errors while pushing code.

When pushing code to the robot, always push the master branch, unless you are testing something on your own branch. At the end of the day / meeting, make sure the robot has the newest code from master pushed to it in case another subteam needs to use the robot.
