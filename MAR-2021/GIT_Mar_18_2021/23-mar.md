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


* To configure the git  :

```
git config --global user.name <username>
git config --global user.email <emailaddress>
git config --list
```
## Untracked and modified changes:
* Untracked is the new file added and it is not there initially.
* Modified is  the file that already present and there are some changes in the content of the file
![preview](../images/git6.png)

* To add only the modified changes to the stagging area:

```
git add -U 
```

```
git add --all   --- it add all changes 
git add -A      --- it add all chnages
git log --oneline   ---it will show u all the commit u have made till now
git checkout <commitid>   --- u can track the changes on the history 
git checkout master 
```
![preview](../images/git7.png)

* Git tracks only the files not the folders .
![preview](../images/git8.png)

# Working on the git 

![preview](../images/git9.png)

## RESET 
* Reset will revert the changes from  the stagging area to the working tree

![preview](../images/git10.png)
![preview](../images/git11.png)