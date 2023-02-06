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

## Scenario : Create a file 1.txt and move from workingarea to Localrepo :
![preview](../images/git4.png)

```
touch 1.txt 

git status 

git add . 

git commit -m "adding 1.txt" 

```

![preview](../images/git5.png)
![preview](../images/G9999.png)


