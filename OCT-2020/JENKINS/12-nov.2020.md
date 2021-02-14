# Failure cases in jenkins:
*  In failure cases we need to look up for mainly two things:
   1. Permissions to the jenkins user (sudo/root).
   2. Command not found . It is issue with the software . We need to check the software is installed or not.

* Create a job in freestyle . provide the git urls and  give _mvn package_ in the execute shell .
![preview](../images/jenkins34.png)
![preview](../images/jenkins35.png)


## Install maven :

```
sudo apt-get update 
sudo apt-get install maven -y 
mvn --version
```

## cron tab syntax:
* We use crontab syntax in two fields in jenkins:
  1. Build periodically 
  2. Poll SCM 
![preview](../images/jenkins36.png)

## If i want my job to be build at 9.0 AM everyday:

```
* 9 * * * 
```
## If i want my job to be build at 9.0 AM everyday sunday:

```
* 9 * * 7 
```

## Difference between build periodically and Poll SCM:
* Build periodically will build  the job at the specific time we defined.
* Poll scm also will build  the job at the specific time we defined, But it will build only when thereare changes in the repositry.
![preview](../images/jenkins37.png)

## Nightly builds  and Day builds:

