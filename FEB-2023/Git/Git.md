* BASIC PIPELINE OF DEVOPS:
![preview](../images/git1.png)

# GIT

* Git is the version control system (VCS)
* Git is developed by **_LINUS TORVALDS_** .


## Organization Expectations :
* All the developers has to work on a same code parallely.
* It must have a feature of versions when the code is being developed.
* Need to have a feature of tracking the changes in the history.
* Must have a ability to serve the application to the mutiple clients.

## GIT HISTORY 
### Evolution of VCS :
  * Share the code via mail.
  * Sharedfolder .
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
          
## Difference betwen Centralised VCS and Distibuted VCS :
![preview](../images/CVCS_VS_DVCS.png)


## prerequisites:
* Install choco :
  [REFER HERE](https://chocolatey.org/docs/installation)

* GIt install
  [REFER HERE](https://chocolatey.org/packages/git.install)

* VSC install
  [REFER HERE](https://chocolatey.org/packages/vscode)

* MOBAXTERM Install 
  [REFER HERE](https://chocolatey.org/packages/MobaXTerm)
  

## THREE phases in git:
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


##  Initializing Git on local  : 

```
 mkdir gitpractice

 cd gitpractice

 git init  ---  To intilalize the git in the present folder.

```
![preview](../images/git3.png)

       

## Scenario : Create a file 1.txt push it from workingarea to Localrepo :
![preview](../images/git4.png)

```
touch 1.txt 

git status 

git add . 

git commit -m "adding 1.txt" 

```
  
![preview](../images/git5.png)
![preview](../images/G9999.png)


## Untracked and Modified :
* Untracked is the new file added and it is not there initially.
* Modified is  the file that already present and there are some changes in the content of the file
![preview](../images/git6.png)


## Add only the modified changes to the stagging area:

```
git add -u      -- add only the modified changes to stagging area 
git add --all   --- it add all changes 
git add -A      --- it add all chnages
```


## Track the changes made in the history : 

```
git log --oneline   ---it will show u all the commit u have made till now
git checkout <commitid>   --- u can track the changes on the history 
git checkout master 
```
![preview](../images/git7.png)


## Will git track folder ..?
* Git tracks only the files not the folders .

![preview](../images/git8.png)


## SCENARIO : Get back the changes from staggingarea to Workingtree & remove the changes from Workingtree also 

![preview](../images/git12.png)

### RESET 
* Reset will get back the changes from  the staggingarea to the workingtree

![preview](../images/git10.png)
![preview](../images/git11.png)

### checkout 
* Checkout  is used to remove the changes made on the workingtree , after we do reset

```
git checkout  <filename>
```
![preview](../images/tt1.png)



## Scenario:  Get back the changes from both staggingarea and workingtree at a sametime  :

```
git reset --hard 
```
![preview](../images/git13.png)

## Removing  the file is also a change in the working of git.
![preview](../images/git14.png)


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


## Head VS Detached Head
* Head will be always at the latest commit .
* When we are going back to the history , the head will be detached and it will go back to the commit which you are using.

![preview](../images/Head.png)
![preview](../images/git15.png)



## Push the changes from local repo to remote repo
###  PUSH 
* git push will add changes from local repo to the remote repo

![preview](../images/git16.png)


* For Remote repository we must have a ***github*** account to create it .
* Repositry is the place where the code will be stored.
* The number of repositries will be depending up on the basis of the project.


## High level view of github 
![preview](../images/git17.png)


## GitHub Signup : [REFER HERE](https://github.com/signup?return_to=https%3A%2F%2Fgithub.com%2Fsignup&source=login) 
* Follow the below instructions to signup :
* **Note** - check the Free plan in the below steps
![preview](../images/h2.png)
![preview](../images/h3.png)
![preview](../images/h4.png)
![preview](../images/h5.png)
![preview](../images/h6.png)
![preview](../images/h7.png)

