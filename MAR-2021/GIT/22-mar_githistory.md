# GIT HISTORY :

## Below are the functionality requirements an organization is expecting :

* All the developers has to work on a same code parallely.
* It must have a feature of versions when the code is being developed.
* Need to have a feature of tracking the changes in the history.
* Must have a ability to server the application to the mutiple clients.

### Evolution of VCS :
  * Share the code via mail.
  * Sharedfolder .
  * Version Control System.
       * First generation :
           * SCCS (Source Code Control System)
           * RCS (Revision Control System)
       * Second Generation :pipa
           * CVS (Concurrent Versions System)
           * SVN (Apache Subversion)
           * Perforce Helix Core
       * Third Generation :
           * Git
* Git is developed by **_LINUS TORVALDS_** .
## Difference betwen Centralised VCS and Distibuted VCS :
![preview](../images/CVCS_VS_DVCS.png)

# Working on git 
```
 mkdir gitpractise

 cd gitpractise

 git init  --- it to intilalize the git in the present folder.

```
![preview](../images/git3.png)

* TO see the changes made are added to the stagging area
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
![preview](../images/git4.png)
![preview](../images/git5.png)

