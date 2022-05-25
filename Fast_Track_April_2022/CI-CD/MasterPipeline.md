# Master Pipeline setup shown in below image :
![preview](../images/sqpipeline.png)

## Requirements:
1. Need a code repo to deploy -- [Gameoflife](https://github.com/devops-surya/game-of-life.git)
2. Required a jenkins-Master with git, maven and ansible installed.
3. Need Jfrog and SonarQube servers and they must be integrated with jenkins-Master.(Makesure SonarScanner installation also takencare)
4. Need to setup ssh connection available between jenkins-Master and deployment server.(To run the ansible-playbook)
![preview](../images/ansible_injenkins.png)
5. Write a Jenkinsfile which has all steps integrated as shown in above __MasterPipeline__ image.

* __Jenkinsfile__
```
pipeline{
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/devops-surya/game-of-life.git'
            }
         }        
       stage('Build'){
            steps{
                sh 'mvn clean package'
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
                   url: 'http://34.222.73.58:8082/artifactory',
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
                                 "target": "MasterPipelineRepo/"

                             }
                                  ]
                   }''',
                        
               )

           }

       }

        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-8.9.2') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
        stage('Running ansible-playbook'){
            steps{
            sh 'ansible-playbook -i /var/lib/jenkins/hosts /var/lib/jenkins/playbook.yml'
            }
        }
       
    }
}
```

* __Playbook.yml__

```
---
- hosts: all
  become: yes 
  tasks: 
    - name: installing java 
      apt:
        name: openjdk-8-jdk
        state: present
        update_cache: yes
    - name: installing tomcat9
      apt:
        name: tomcat9
        state: present 
        update_cache: yes
    - name: copying the war file
      copy:
        src: /var/lib/jenkins/workspace/Masterpipeline/gameoflife-web/target/gameoflife.war
        dest: /var/lib/tomcat9/webapps/
    - name: restart the tomcat9
      service:
        name: tomcat9
        state: restarted
```

* Check the application working on browser as shown in below:

```
http://<publicip>:8080/gameoflife
```

![preview](../images/golbrowser.png)



<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>