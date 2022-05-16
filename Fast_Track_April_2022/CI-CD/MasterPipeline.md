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
        stage('Running ANsible-playbook'){
            sh 'ansible-playbbok -i /var/lib/jenkins/hosts /var/lib/jenkinsplaybook.yml'
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
        src: /home/devops/SampleWebApp.war
        dest: /var/lib/tomcat9/webapps/
    - name: restart the tomcat9
      service:
        name: tomcat9
        state: restarted
```