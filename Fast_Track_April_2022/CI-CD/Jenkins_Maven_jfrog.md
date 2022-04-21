# JENKINS and MAVEN
* Jenkins is a ci/cd tool
* ci -- continous integration 
* cd -- continous delivery / continous deployment

## Basic flow of devops :
![preview](../images/jenkins1.png)
![preview](../images/jenkins2.png)
![preview](../images/jenkins3.png)


# Installing jenkins 
* prerequisites:
1. Ubuntu
2. Java 
3. Jenkins

## For installing jenkins we have two ways.
1. Jenkins master 
2. Quick setup (it is not the enterprize setup)
* For quick setup [REFER HERE](https://www.jenkins.io/download/)
```
 java-jar <path to the download>
```
## For installing jenkins master :
* For the jenkins installation [REFER HERE](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) 



```
sudo apt-get update
sudo apt-get install openjdk-8-jdk

java -version

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

* To open jenkins on brower 

```
http://ipaddress:8080
```
* After iusing above command we will get below screen on browser:
![preview](../images/jenkins4.png)
 * copy the password and paste it on the browser:
![preview](../images/jenkins5.png)
* CLick on the install suggested plugins , then u will see below page:
![preview](../images/jenkins6.png)
* provide the username, password , email:
![preview](../images/jenkins7.png)
* After providing usename and password click on the save and continue:
![preview](../images/jenkins8.png)
* Main page of jenkins
![preview](../images/jenkins9.png)

## To create a new job , we wil use new item:
![preview](../images/jenkins10.png)

## Manage jenkins is used to configure the jenkins (settings)
![preview](../images/jenkins11.png)

## jenkins executor :
* Executor will define , how many jobs run parallely at a time.
![preview](../images/jenkins12.png)

## To  create a job , we have multiple ways .Refer below screen shot:
![preview](../images/jenkins13.png)

### Creating a new jon in FREESTYLE:
* click on the newitem and follow the below screenshots :
![preview](../images/jenkins14.png)
![preview](../images/jenkins15.png)
![preview](../images/jenkins16.png)
![preview](../images/jenkins17.png)


# Installing jenkins 
* prerequisites:
1. Ubuntu
2. Java 
3. Jenkins

## For installing jenkins we have two ways.
1. Jenkins master 
2. Quick setup (it is not the enterprize setup)
* For quick setup [REFER HERE](https://www.jenkins.io/download/)
```
 java-jar <path to the download>
```
## For installing jenkins master :
* For the jenkins installation [REFER HERE](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) 



```
sudo apt-get update
sudo apt-get install openjdk-8-jdk

java -version

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```

* To open jenkins on brower 

```
http://ipaddress:8080
```
* After iusing above command we will get below screen on browser:
![preview](../images/jenkins4.png)
 * copy the password and paste it on the browser:
![preview](../images/jenkins5.png)
* CLick on the install suggested plugins , then u will see below page:
![preview](../images/jenkins6.png)
* provide the username, password , email:
![preview](../images/jenkins7.png)
* After providing usename and password click on the save and continue:
![preview](../images/jenkins8.png)
* Main page of jenkins
![preview](../images/jenkins9.png)

## To create a new job , we wil use new item:
![preview](../images/jenkins10.png)

## Manage jenkins is used to configure the jenkins (settings)
![preview](../images/jenkins11.png)

## jenkins executor :
* Executor will define , how many jobs run parallely at a time.
![preview](../images/jenkins12.png)

## To  create a job , we have multiple ways .Refer below screen shot:
![preview](../images/jenkins13.png)

### CREATING A NEW JOB IN FREESTYLE:
* click on the newitem and follow the below screenshots :
![preview](../images/jenkins14.png)
![preview](../images/jenkins15.png)
![preview](../images/jenkins16.png)
![preview](../images/jenkins17.png)

# Build tools
   * c => Make, GCC
   * Java => Ant, Maven, Gradle
   * .net => MSBuild, dotnet build

* For maven projects , we are going to have POM.XML , in which developer defines the dependencies to build the project and also he will define the output of the build.
![preview](../images/jenkins38.png)
![preview](../images/jenkins39.png)  
![preview](../images/jenkins40.png) 

## MAVEN GOALS:
  * compile
  * Test
  * package
  * Install
  * clean
# compile: 
* when we are firing the command __mvn compile__.This creates the  classfile.

# Test:  __mvn test__
* This executes the junit tests.

# package :  __mvn package__
* This will create the package (.war/.jar/.ear)

# clean :  __mvn clean__
* when you do clean , it will delete the old war and create the war.
* Basically the output will be stored in the target folder.

```
mvn test = mvn compile + mvn test
mvn package = mvn compile + mvn test + mvn package

```

* Jenkins is having a maven plugin called __invoke top-levl maven plugin__
![preview](../images/jenkins41.png) 
![preview](../images/jenkins42.png) 
![preview](../images/jenkins43.png)
![preview](../images/jenkins44.png)  
![preview](../images/jenkins45.png) 

* Delete workspace before every buils , if it is checked it is going to rmove the whole workspca for every build.
![preview](../images/jenkins46.png)



# Create a job for GOL build.
1. create a freestyle job with name __gol__
2. SCM -- provide the github url 
3. POLLSCM --- * * * * *
4. DELETE the workspace for every build
5. BUILD -- provide the goal in the invoke top-level maen plugin.

![preview](../images/jenkins47.png)

![preview](../images/jenkins48.png)

5. BUild the job.

![preview](../images/jenkins49.png)

6. GO to configure and add post build actions as below:

![preview](../images/jenkins50.png)

7. Build the job again and ouput will be as below:

![preview](../images/jenkins51.png)

* Artifacts are nothing but the war/jar/ear files.

8. Go to configure and add the publish junit test resulta as below:

![preview](../images/jenkins52.png)

9. BUild the job and output will be as shown below:

![preview](../images/jenkins53.png)


## Restarting the jenkins :
* Multiple ways to restart 
  1. In cli 
    ``` 
    sudo service jenkins restart 
    ```
  2. FROM GUI 
    ![preview](../images/jenkins54.png)
  3. In manage jenkins
     ![preview](../images/jenkins55.png)

## Configurations in the __ Manage jenkins__
* IN manage jenkins => configure system 

![preview](../images/jenkins56.png)

![preview](../images/jenkins57.png)

* IN manage jenkins => configure global security 

![preview](../images/jenkins58.png)

* IN manage jenkins => manage plugins

![preview](../images/jenkins59.png)

# Adding a Node to the jenkins:
* For understanding the node concept. refer below image :

![preview](../images/jenkins60.png)

## Basic image of jenkins amster and node:

![preview](../images/jenkins61.png)

* To add the node to the jenkins as per the above image. Did the ssh-keygen as below:

![preview](../images/jenkins62.png)

## In jenkins to add the node.

* In manage jenkins => mange nodes 

![preview](../images/jenkins63.png)

![preview](../images/jenkins64.png)

![preview](../images/jenkins65.png)

![preview](../images/jenkins66.png)

![preview](../images/jenkins67.png)

## Using node on the jenkins job:

![preview](../images/jenkins68.png)

![preview](../images/jenkins69.png)

## Backup of jenkins:
![preview](../images/jenkins70.png)

![preview](../images/jenkins71.png)

![preview](../images/jenkins72.png)

![preview](../images/jenkins73.png)

![preview](../images/jenkins74.png)

# Adding node to the jenkins:

![preview](../images/jenkins75.png)

## Below are the high level steps discussed on the freestyle:
1. Git 
2. Invoke top level maven plugin
3. archive the artifacts
4. publish the junit reports
5. Running the ansible playbook.

## Creating a jenkins job in pipeline format:
![preview](../images/jenkins76.png)

![preview](../images/jenkins77.png)


* Basic syntax on the groovy:

```
node('<LABEL>'){
    stage('git clone'){
      
    }
    stage('build the code){

    }
    stage('archive the artifacts'){

    }
    stage('publish the junit reports'){

    }
    stage('Running the ansible playbook'){
        
    }
}
  
```

# Jenkins pipeline :
* In jenkins pipeline there are two ways:
  1. pipeline  script     
  2. pipeline  script from SCM

* The approcah we follow for the jenkins pipeline and writing the groovy for is called as pipeline-as-code.

## Basic script :
```
node('ubuntu'){
    stage('git clone'){
      git 'https://github.com/devops-surya/game-of-life.git' 
    }
    stage('build the code'){
      sh 'mvn package'
    }
    stage('archive the artifacts'){
      archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
    }
    stage('publish the junit reports'){
      junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
}
```
## Snippet generator:
![preview](../images/jenkins78.png)

## To generate the pipeline script for git:
![preview](../images/jenkins79.png)

## To generate pipeline for the publish junkts tests:
![preview](../images/jenkins80.png)


* The output of the jenkins pipeline job will be as below:
![preview](../images/jenkins81.png)

## Job Configuration History :
* This plugin is used to tarck the changes made previously  .
![preview](../images/jenkins82.png)

## Jenkinsfile 
* Using jenkins will be helpful in tracking the changes .

## scripted pipeline vs declarative pipeline :
*  scripted pipeline:
```
node('ubuntu'){
    stage('git clone'){
      git 'https://github.com/devops-surya/game-of-life.git' 
    }
    stage('build the code'){
      sh 'mvn package'
    }
    stage('archive the artifacts'){
      archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
    }
    stage('publish the junit reports'){
      junit 'gameoflife-web/target/surefire-reports/*.xml'
    }
}
```

* Declarative pipeline:
```
pipeline {
   agent { label 'ubuntu' }
   stages{
       stage('git clone'){
           steps{
               git 'https://github.com/devops-surya/game-of-life.git'  
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
           
       }

   }
}
```

## Create a new pipeline job with pipeline script from scm as below:

![preview](../images/jenkins83.png)
![preview](../images/jenkins84.png)

## Blue ocean plugin :
* In manage jenkins => manage plugins => available => Blue ocean
* After installing u r going to see below changes:
![preview](../images/jenkins85.png)
![preview](../images/jenkins86.png)

* Declarative pipeline:
```
pipeline {
   agent { label 'ubuntu' }
   stages{
       stage('git clone'){
           steps{
               git 'https://github.com/devops-surya/game-of-life.git'  
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
           
       }

   }
}
```

## Create a new pipeline job with pipeline script from scm as below:

![preview](../images/jenkins83.png)
![preview](../images/jenkins84.png)

## Blue ocean plugin :
* In manage jenkins => manage plugins => available => Blue ocean
* After installing u r going to see below changes:
![preview](../images/jenkins85.png)
![preview](../images/jenkins86.png)

# FORK:

![preview](../images/jenkins87.png)

* Go to the repo from which you want to fork:

![preview](../images/jenkins88.png) 

![preview](../images/jenkins89.png)


## Build with parameters:

![preview](../images/jenkins90.png)

* Install the plugin shown in below image:
![preview](../images/jenkins91.png)

* Ater install we see can the option in parameteres:
![preview](../images/jenkins92.png)

![preview](../images/jenkins93.png)

![preview](../images/jenkins94.png)

![preview](../images/jenkins95.png)

* To trigger the jenkins jobs from aone-to-another:
  * Install the plugin shown in the below image:
![preview](../images/jenkins97.png)

* For installing we can see the below options on the jenkins UI:
    ![preview](../images/jenkins98.png)
    ![preview](../images/jenkins99.png)

# SNAPSHOT vs RELEASE 
* If you find the a artifacts with the Snapshot , that means it is still in development.
* If you find your artifact with the release , that means it is ready for the deploymnet and sent it to production.

EX: Game-of-life.war-sanapshot-1.0 
EX: Game-of-life.war-Release-1.0

# Upstream and Downstream projects:
![preview](../images/jenkins100.png)
![preview](../images/jenkins101.png)


### Jenkins declarative pipeline syntax:
* For the pipeline syntax refer the link [REFER HERE](https://www.jenkins.io/doc/book/pipeline/syntax/)

## For git pipeline syatax [REFER HERE](https://www.jenkins.io/doc/pipeline/steps/git/)

```
pipeline {
   agent any
   stages{
       stage('git clone'){
           steps{
               git branch: 'master', url: 'https://github.com/devops-surya/game-of-life.git'
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
           
       }

   }
}
```

## Triigers for build peridically and pollSCM in the pipeline job [REFER HERE](https://www.jenkins.io/doc/book/pipeline/syntax/#triggers)

```
pipeline {
   agent any
   triggers{
      cron('* * * * *')
   }
   triggers{
      pollSCM('* 8 * * *')
   }
   stages{
       stage('git clone'){
           steps{
               git branch: 'master', url: 'https://github.com/devops-surya/game-of-life.git'
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
           
       }

   }
}
```

## UPSTREAM job triggering:

```
pipeline {
   agent any
   triggers{
     upstream(upstreamProjects: 'pipeline-1', threshold: hudson.model.Result.SUCCESS)
   }
   stages{
       stage('git clone'){
           steps{
               git branch: 'master', url: 'https://github.com/devops-surya/game-of-life.git'
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
           
       }

   }
}
```

## Parameters using in jenkins pipeline [REFER HERE](https://www.jenkins.io/doc/book/pipeline/syntax/#parameters)
```


```

### Building the another job from this present job [REFER HERE](https://www.jenkins.io/doc/pipeline/steps/pipeline-build-step/)
```
pipeline {
   agent any
   triggers{
     upstream(upstreamProjects: 'pipeline-1', threshold: hudson.model.Result.SUCCESS)
   }
   parameters{
     string(name: 'BUILD_BRANCH', defaultValue: 'master', description: 'parameterized the branch' )
   }
   stages{
       stage('git clone'){
           steps{
               git branch: "$BUILD_BRANCH", url: 'https://github.com/devops-surya/game-of-life.git'
           }        
       }
       stage('build the code'){
           steps{
              sh 'mvn package'
           }
       }
       stage('archive the artifacts'){
           steps{
              archiveArtifacts artifacts: 'gameoflife-web/target/*.war', followSymlinks: false
           }          
       }
       stage('publish the junit reports'){
           steps{
              junit 'gameoflife-web/target/surefire-reports/*.xml'
           }
	   stage('triggering the another job named gol'){
	       steps{
		      build job: 'gol'
		   }
	   }
           
       }

   }
}
```

## Multibranch pipeline:

![preview](../images/jenkins102.png)

![preview](../images/jenkins103.png)



### Jfrog artifactory :
* To install the jfrog [REFER HERE](https://jfrog.com/open-source/#artifactory)
![preview](../images/jenkins104.png)

* After downloading that you  need copy that to the machine where you  want to install artifactory:
 1. In your local machine , copy the jfrog-artifactory-oss-7.10.6.deb to the path documents => mobaxterm => home 
 2. copy to the artifactory machine
    ```
     scp -i <pemfilepath> jfrog-artifactory-oss-7.10.6.deb   ubuntu@<publicip>:/home/ubuntu/
     ```
 3. After copying to the artifactory machine follow below commads:
    ```
    sudo dpkg -i jfrog-artifactory-oss-7.10.6.deb
    systemctl enable artifactory
    sudo systemctl start  artifactory
    ```
  4. OPen artifactory in UI
    ```
    http://publicip:8081/artifactory
    ```
    ![preview](../images/jenkins105.png)
  5. Give the username and password.
  ```
  Username: admin
  Password: password
  ```
  ![preview](../images/jenkins106.png)
  * It will ask for change password:
  ![preview](../images/jenkins107.png)

  * To create repositry see below steps:
  ![preview](../images/jenkins108.png)

  ![preview](../images/jenkins109.png)

  ![preview](../images/jenkins110.png)

  ![preview](../images/jenkins111.png)

  6. Make sure that artifactory plugin is installed before doing the jforgintegartion with jenkins
   ![preview](../images/jenkins116.png)

  7. To integrate JFROG with the jenkins , follow below steps:
      Managejenkins => configure system => artifactory
    ![preview](../images/jenkins112.png)
  8. Cretae a maven project by following below steps:
     ![preview](../images/jenkins113.png)
     ![preview](../images/jenkins114.png)
     ![preview](../images/jenkins115.png)
  9. Build the job and check the jfor artifactory repo :
     ![preview](../images/jenkins117.png)

* For the  jforg ansible module  [REFER HERE](https://docs.ansible.com/ansible/latest/collections/community/general/maven_artifact_module.html)

* For the Jfrog to be added in the Jenkinsfile declarative pipeline [REFER HERE](https://www.jfrog.com/confluence/display/RTF6X/Declarative+Pipeline+Syntax)

