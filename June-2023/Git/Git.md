# GIT :

## Organization Requirements :
* All the developers has to work on a same code parallely.
* It must have a feature of versions when the code is being developed.
* Need to have a feature of tracking the changes in the history.
* Must have a ability to serve the application to the mutiple clients.

<br/>

* * * 

<br/>

## GIT HISTORY 
### Evolution of VCS :
  * Share the code via mail.
  * Sharedfolder.
  * Version Control System.
       * First generation :
           * SCCS (Source Code Control System)
           * RCS (Revision Control System)
       * Second Generation :
           * CVS (Concurrent Versions System)
           * SVN (Apache Subversion)
           * Perforce Helix Core
       * Third Generation :
           * Git
          
<br/>

* * * 

<br/>

# GIT

* Git was developed by ___Linus Torvalds___, the creator of the Linux operating system. In 2005, Torvalds began working on Git to address the version control needs of the Linux kernel development community. He wanted a distributed version control system that would be fast, efficient, and capable of handling the large and complex codebase of the Linux kernel. Torvalds released the initial version of Git in April 2005, and since then, it has gained widespread adoption and become one of the most popular version control systems in the software development industry.

* Git is a distributed version control system (VCS) that allows multiple people to collaborate on a project simultaneously. It was created by Linus Torvalds, the creator of the Linux operating system, in 2005. Git is widely used in software development to manage source code and track changes made to files over time.

* Here are some key concepts and features of Git:

    * Version Control: Git tracks changes to files and keeps a history of all modifications. This enables developers to revert to previous versions, compare changes, and collaborate effectively.

    * Distributed System: Unlike centralized version control systems, Git is distributed. Each developer has a complete copy of the repository, including the entire history. This allows for offline work and makes it easy to merge changes from multiple sources.

    * Repositories: A Git repository is a collection of files and their complete history. It contains the entire project, including branches, tags, and commits. Repositories can be stored locally or hosted remotely on services like GitHub, GitLab, or Bitbucket.

    * Commits: A commit represents a snapshot of the project at a specific point in time. It captures the changes made to the files, along with a commit message describing the modifications. Commits are organized in a directed acyclic graph, forming a history of the project.

    * Branches: Git allows the creation of branches, which are independent lines of development. Branches enable developers to work on separate features or experiments without affecting the main codebase. They can be merged back into the main branch when the changes are ready.

    * Merging and Conflict Resolution: Git provides tools for merging changes from different branches into a single branch. In some cases, conflicts may arise when the changes overlap. Git offers mechanisms to resolve conflicts manually, ensuring that the final result is accurate.

    * Remote Repositories: Git facilitates collaboration by allowing repositories to be hosted on remote servers. Developers can push their local changes to the remote repository or pull changes made by others. This enables seamless teamwork and easy synchronization.

* Git has become an industry-standard tool for version control due to its flexibility, speed, and powerful features. It is widely used not only in software development but also in other fields where tracking changes and collaborating on projects is crucial.




<br/>

* * * 

<br/>





## Difference betwen Centralised VCS and Distributed VCS :
![preview](../images/CVCS_VS_DVCS.png)

<br/>

* * * 
<br/>

## Prerequisites:
* Install choco :
  [REFER HERE](https://chocolatey.org/docs/installation)

* GIt install
  [REFER HERE](https://chocolatey.org/packages/git.install)

* MOBAXTERM Install 
  [REFER HERE](https://chocolatey.org/packages/MobaXTerm)
  
<br/>

* * * 
<br/>

## Three phases in git:
1. Working tree
2. Stagging area
3. Local repo
4. Remote repo .

![preview](../images/git2.png)

* To see the changes made 
```
git status
```

* To add all the changes to the staging area 
```
git add .
```

* To commit all the changes to the local repo 

```
git commit -m "< added some changes>"
```

<br/>

* * * 
<br/>

##  Initializing Git on local  : 

```
 mkdir gitpractice

 cd gitpractice

 git init  ---  To intilalize the git in the present folder.

```
![preview](../images/git3.png)

<br/>

* * * 
<br/>  

# Move changes from workingtree to Localrepo
## Scenario : Create a file 1.txt move it from workingtree to Localrepo :
![preview](../images/git4.png)

```
touch 1.txt 

git status 

git add . 

git commit -m "adding 1.txt" 

```
  
![preview](../images/git5.png)
![preview](../images/G9999.png)

<br/>

* * * 
<br/>

## Untracked and Modified files :
* Untracked is the new file added and it is not there initially.
* Modified is the file that already present and there are some changes in the content of the file
![preview](../images/git6.png)

<br/>

* * * 
<br/>

## Add only the modified changes to the stagging area:

```
git add -u      -- add only the modified changes to stagging area 
git add --all   --- it add all changes 
git add -A      --- it add all chnages
```
<br/>

* * * 
<br/>

## Track the changes made in the history : 

```
git log --oneline   ---it will show u all the commit u have made till now
git checkout <commitid>   --- u can track the changes on the history 
git checkout master 
```
![preview](../images/git7.png)

<br/>

* * * 
<br/>

## Will git track folder ..?
* Git tracks only the files not the empty folders .

![preview](../images/git8.png)

<br/>

* * * 
<br/>

# Revert the changes from Staggingarea to Workingtree & delete in  Workingtree 
## SCENARIO : Get back the changes from staggingarea to Workingtree & remove the changes from Workingtree also 

![preview](../images/git12.png)

### RESET 
* Reset will get back the changes from the staggingarea to the workingtree

![preview](../images/git10.png)
![preview](../images/git11.png)

<br/>

* * * 
<br/>

### checkout 
* Checkout  is used to remove the changes made on the workingtree , after we do reset
* **NOTE** : Checkout in this case works on modified files 

```
git checkout  <filename>
```
![preview](../images/tt1.png)

<br/>

* * * 
<br/>

## Scenario:  Get back the changes from both staggingarea and workingtree at a sametime  :

```
git reset --hard 
```
![preview](../images/git13.png)

<br/>

* * * 
<br/>

#  Tracking the deleted files
## Removing  the file is also a change in the working of git.
![preview](../images/git14.png)

<br/>

* * * 
<br/>

## SCENARIO: Revert the commit .
![preview](../images/gn9.png)


### Revert :
* Git revert is to revert the commit .

```
touch 7.txt

git add .

git commit -m " added 7.txt"

git revert <commitid>
```

![preview](../images/gn7.png)
![preview](../images/gn8.png)

<br/>

* * * 
<br/>

## Head VS Detached Head
* Head will be always at the latest commit .
* When we are going back to the history , the head will be detached and it will go back to the commit which you are using.

![preview](../images/Head.png)
![preview](../images/git15.png)

<br/>

* * * 
<br/>

## Push the changes from local repo to remote repo
###  PUSH 
* git push will add changes from local repo to the remote repo

![preview](../images/git16.png)


* For Remote repository we must have a ***github*** account to create it .
* Repositry is the place where the code will be stored.
* The number of repositries will be depending up on the basis of the project.


## High level view of github 
![preview](../images/git17.png)

<br/>

* * * 
<br/>

## GitHub Signup : [REFER HERE](https://github.com/signup?return_to=https%3A%2F%2Fgithub.com%2Fsignup&source=login) 
* Follow the below instructions to signup :
* **Note** - check the Free plan in the below steps
![preview](../images/h2.png)
![preview](../images/h3.png)
![preview](../images/h4.png)
![preview](../images/h5.png)
![preview](../images/h6.png)
![preview](../images/h7.png)

<br/>

* * * 
<br/>

## Create a repositry in the github:
* Go to the repositries and then refer the image below:
![preview](../images/git19.png)
* Provided the repositry name and make it public , so that it will be available to everyone.
![preview](../images/git20.png)

## Configure RemoteRepo to the LocalRepo to push the code. 

![preview](../images/git21.png)

* To configure the git in your local  :

```
git config --global user.name <username>
git config --global user.email <emailaddress>
git config --list
git remote add origin https://github.com/devops-surya/sample.git
git push origin master
```
![preview](../images/git22.png)

<br/>

* * * 
<br/>

## PersonalAccessTokens
* Git depricated the support of using password and  expecting us to use the PersonalAccessToekn as password.
* Go to >> Settings >> Developer Settings >> Personal access tokens >> Generate New Token >> 1.Note 2.Expiration 3.select scopes 4. Generate Token

![preview](../images/gn1.png)
![preview](../images/gn2.png)
![preview](../images/gn3.png)
![preview](../images/gn4.png)
![preview](../images/gn5.png)
![preview](../images/gn6.png)

<br/>

* * * 
<br/>

# CLONE
*  you can use the git clone command followed by the repository URL to clone the repository. The repository URL can be obtained from the repository's webpage or by copying the URL provided by the version control system hosting the repository (e.g., GitHub, GitLab, Bitbucket).

## Scenario : A new developer added to a team and he/she want the  total code from the repositry:

```
git clone https://github.com/devops-surya/sample.git
```
![preview](../images/git23.png)
<br/>

* * * 
<br/>

# PULL & FETCH
* The git pull command is used to update your local repository with the latest changes from the remote repository. It combines the actions of ```git fetch``` and ```git merge``` into one command.

```
git pull = git fetch + git merge
```

## Scenario : A developer already exists and he/she has the code in his local desktop. But he/she don't have the latest code. To get the latest the code we use git pull

```
git pull https://github.com/devops-surya/sample.git
```
<br/>

* * * 
<br/>
 

## Multi branching :
* If a company want to serve the code to the mutliple companies , they will create multiple branches and go for the parallel development.
![preview](../images/git335.png)

* To create a branch

```
git branch <branchname>
```
* To list the branches:
```
git branch
```

* To switch between the branches

```
git checkout <branchname>
```

* To create a branch and switch to it directly:

```
git checkout -b <branchname> 
```
![preview](../images/git36.png)
![preview](../images/git37.png)

* To push the code from the company-x branch to the remote repo:

```
git push origin company-x
```
![preview](../images/git38.png)
![preview](../images/git39.png)

* To see the remote branches:
```
git branch -r
```
![preview](../images/git40.png)

<br/>

* * * 
<br/>


## MERGE :
* Merge will be helpful in combining the code between two branches .

![preview](../images/git41.png)
* create a file y1.txt and do add , commit .
![preview](../images/git42.png)
* Switch to the company-x branch . Create  a file x1.txt and do add , commit .
![preview](../images/git43.png)

<br/>

* * * 
<br/>



## Merge conflicts.
* A merge conflict is a situation that occurs in Git when there are conflicting changes to the same part of a file or multiple files during a merge operation.

## Scenario : We have two developers newly assigned to a new project.

![preview](../images/git334.png)

* To create the above scenario , follow the below steps :
  * Create a folder of mergeconflicts.
  * create a two folders with names developer1 , developer2 .
  * Get into folders of developer1, developer2 and clone the repo .
  ![preview](../images/g1.png)
  * Developer1 has made some changes to the file 6.txt and then pushed to the repo .
  ![preview](../images/g2.png) 
  * Developer2 has made changes on the local and pushed the changes , here it is asking for the pull as shown below :
  ![preview](../images/g3.png) 
  * Developer2 has to pull the code and has to take call of merge conflicts and push the code again.
  ![preview](../images/g4.png)
  
<br/>

* * * 
<br/>



## Fastforward merge:
![preview](../images/git45.png)
* Create branch a company-z. create a file z1.txt and do add , commit.
![preview](../images/git44.png)
* if u dont want to go with the fastforward merge 

```
git checkout master 
git merge --no-ff company-z
```
<br/>

* * * 
<br/>

## Rebase :
* Rebase will be used when you want to change the base of the branch.
![preview](../images/git47.png)
* Create  a branch-a and create a a1.txt file in it. do git add , git commit.
* switch to master branch and create file rebase.txt, do git add and git commit.
![preview](../images/git46.png)
* For rebase to be done

```
git checkout branch-a
git rebase master
```
![preview](../images/git48.png)

<br/>

* * * 
<br/>

## cherry-pick :
* Cherry-pick will be used when you need the specific commit from another branch.
![preview](../images/git50.png)
* Create a branch-c , add two commits  by creating c1.xtx and c2.txt.
![preview](../images/git49.png)
* Create a branch-d , add d1.txt . do add and commit.
![preview](../images/git51.png)
![preview](../images/git52.png)

<br/>

* * * 
<br/>

# Delete a Branch in Local/Remote:

## Delete Local branch 

* -d --> Delete 
* -D --> Force Delete

```
git branch -d branch_name    
git branch -D branch_name
```

### Delete Remote branch 

* -d --> Delete 
* -D --> Force Delete

```
git push origin -d branch_name
git push origin -D branch_name
```

<br/>

* * * 
<br/>


## Branching strategy :
![preview](../img/BranchingStarategy.png)


<br/>

* * * 
<br/>


## Fork:
* A fork creates a completely independent copy of Git repository that sits in your github account.

![preview](../images/jenkins87.png)

* Go to the repo  which you want to fork:

![preview](../images/jenkins88.png) 

![preview](../images/jenkins89.png)


<br/>

* * * 
<br/>

## STASH 
* ```git stash`` is a Git command used to temporarily save changes that are not ready to be committed yet. It allows you to switch to a different branch or work on a different task without committing your current changes. The changes you stash are stored in a stack of stashes, and you can apply or drop them later.

* The basic usage of git stash is as follows:

```
touch stash.txt
git stash 
```
![preview](../img/git1.png)

* To apply the most recent stash and remove it from the stash stack, you can use ```git stash pop```:

```
git stash pop

```
![preview](../img/git2.png)


* To apply the stash without removing it from the stash stack, you can use ```git stash apply```:

```
git stash apply
```
![preview](../img/git3.png)
![preview](../img/git4.png)


<br/>

* * * 
<br/>

## Blame :
* In Git, the ```blame``` command is used to track the changes made to a file, displaying the author and commit information for each line of the file. It helps you determine who last modified a specific line or section of code, providing valuable insights into the commit history.

    * The basic syntax of git blame is as follows:

    ```
    git blame <file>

    ```

<br/>

* * * 
<br/>
