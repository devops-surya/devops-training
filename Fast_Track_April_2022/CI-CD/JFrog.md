# JFrog Artifactoy:
* JFrog Artifactory is the Universal Repository Manager supporting all major packaging formats, build tools and CI servers.

### Pipeline integration with Jfrog  :
![preview](../images/jfpipeline.png)


## Install JFrog Artifactory oss :
* Installation steps [REFERHERE](https://www.devopsschool.com/blog/artifactory-install-and-configurations-guide/#:~:text=Artifactory%20Pro%20Install%20in%20Linux%20using,jfrog/artifactory/var/etc/system.yaml)

```
# find the release name
lsb_release -c
distribution="focal" #ubuntu 20.04
wget -qO - https://releases.jfrog.io/artifactory/api/gpg/key/public | sudo apt-key add -;
echo "deb https://releases.jfrog.io/artifactory/artifactory-debs {distribution} main" | sudo tee -a /etc/apt/sources.list;
sudo apt-get update && sudo apt-get install jfrog-artifactory-oss -y
sudo systemctl enable artifactory.service
sudo systemctl start artifactory.service
sudo systemctl status artifactory.service

echo "deb https://releases.jfrog.io/artifactory/artifactory-debs focal main" | sudo tee -a /etc/apt/sources.list;

```

* Access artifactory by using : __http://publicip:8081__ and follow the below steps:
* Default username and password :
```
Username: admin
Pasword : password
```
![preview](../images/jf1.png)
![preview](../images/jf2.png)
![preview](../images/jf3.png)
![preview](../images/jf4.png)

* Create a repository :
![preview](../images/jf5.png)
![preview](../images/jf6.png)
![preview](../images/jf7.png)
![preview](../images/jf8.png)
![preview](../images/jf9.png)


### Integrate Jfrog with the jenkins :
* Install Jfrog plugon from __manage plugin__
![preview](../images/jf10.png)

* After plugin installated, Navigate to Manage jenkins >> Configure System , do the changes as below and save them
![preview](../images/jf11.png)
![preview](../images/jf12.png)


## Create a Maven-job to store our artifacts to the jfog artifactory:
1. Create a new maven job 
![preview](../images/jf13.png)

2. SCM - provide code repository
![preview](../images/jf14.png)

3. Build -- Provide maven goal 
![preview](../images/jf15.png)

4. Post-build-Actions -- Deploy Artifacts to Artifactory
![preview](../images/jf16.png)
![preview](../images/jf17.png)

5. Build the maven-job to check the artifactory working as per expexted.
![preview](../images/jf18.png)
![preview](../images/jf19.png)

* Upload the artifacts to jfrog in Declarative-pipeline :
* Reference Document for __Jfrog Ppeline syntax__ [REFERHERE](https://www.jfrog.com/confluence/display/JFROG/Declarative+Pipeline+Syntax)

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
       stage('rt server'){
           steps{
               rtServer (
                   id: 'JFROG-OSS',
                   url: 'http://35.89.142.196:8082/artifactory',
                   username: 'admin',
                   password: 'Jfrog@123',
                   bypassProxy: true,
                   timeout: 300
               )

           }
       }
       stage('rt upload'){
           steps{
               rtUpload (
                   serverId: 'JFROG-OSS',
                   spec: '''{
                         "files": [
                             {
                                 "pattern": "gameoflife-web/target/*.war",
                                 "target": "my-second-repo/"

                             }
                                  ]
                   }''',
                        
               )

           }

       }

      }


    }


```

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

