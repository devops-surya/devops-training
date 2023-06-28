# Jenkins:
* Jenkins is an open source __continuous integration/continuous delivery and deployment__ (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.
* Jenkins is a CI/CD tool
    * ***CI (Continous integration)*** : Continuous Integration is the practice of merging code changes into a shared repository frequently and automatically verifying that the resulting code builds, tests, and integrates successfully.
    * ***CD -- Continous Delivery / Continous Deployment*** :
        * **Continous Delivery** : Continuous Delivery is a software development practice that aims to make the release process more efficient and reliable by automating the entire software delivery pipeline. The idea is to ensure that code changes are always in a releasable state and can be deployed to production at any time. Continuous Delivery typically involves a continuous integration process that compiles and tests the code, followed by an automated deployment process that deploys the built artifacts to a staging environment. Once the code has been successfully tested in the staging environment, it can be promoted to the production environment.
        * **Continous Deployment** : Continuous Deployment, on the other hand, is a practice where every code change that passes the automated tests is automatically deployed to production. This means that any changes made to the code are automatically released to the users without any human intervention. Continuous Deployment is a more advanced version of Continuous Delivery and is generally suitable for organizations with high release frequency and the ability to handle fast feedback loops.
<br/>

* * * 

<br/>

## Pipeline flow of devops :
![preview](../images/jenkins1.png)
![preview](../images/JenkinsBasicPipeline.png)
![preview](../images/CI_CDPipeline1.png)

<br/>

* * * 

<br/>

## Installing Jenkins 
### prerequisites:
1. Ubuntu Server 
2. Java 
3. Jenkins

## For installing Jenkins we have two ways.
1. Quick setup (it is not the enterprize setup)
2. Jenkins master 

### Quick setup [REFER HERE](https://www.jenkins.io/download/)
```
 java-jar <path to the download>
```

### Jenkins master setup :
* Jenkins installation official document [REFER HERE](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu) 
* Create a EC2 in AWS and follow below steps to install Jenkins :

#### Java installation:
```
sudo apt-get update
sudo apt-get install openjdk-11-jdk

java -version
```
#### jenkins Installation:
```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

### To open Jenkins on browser :
* ___NOTE___: Jenkins runs on port of 8080 . So port 8080 must be opened in EC2 server (or) set inbound rule to All Traffic .
```
http://publicipaddress:8080
```
* ***http://publicipaddress:8080*** will open below screen on browser:
![preview](../images/J4.png)
* Copy the password from server and paste it on the browser:
![preview](../images/J5.png)
![preview](../images/J6.png)
* Select ***Install suggested plugins*** and wait all plugins installed:
![preview](../images/J7.png)
![preview](../images/J8.png)
* ***Create First Admin User*** by provide the username, password , email then  Save and continue:
![preview](../images/J9.png)
* ***Instance Configuration*** -- No changes
![preview](../images/J10.png)
![preview](../images/J11.png)
* Dashboard of jenkins
![preview](../images/J12.png)


<br/>

* * * 

<br/>


## Create a *Job* :
* In Jenkins we do automation by creating jobs :
![preview](../images/J13.png)

## Multiple ways to create a Job:
![preview](../images/J14.png)

## Create a Job in Freestyle:
* Click on the  **New Item**  and follow the below instructions in the screenshots :
![preview](../images/J13.png)
![preview](../images/J15.png)
![preview](../images/J16.png)
![preview](../images/J17.png)
![preview](../images/J18.png)




<br/>

* * * 

<br/>


## Multiple Sections in Jenkins Freestyle job:
1. General
2. Source Code Management
3. Build Triggers
4. Build Environment
5. Build Steps
6. Post-build Actions
![preview](../images/J22.png)
![preview](../images/j23.png)


<br/>

<br/>

* * * 

<br/>

<br/>



# Explore ***Manage Jenkins*** Options : 

## ***Manage jenkins*** is used to configure the Jenkins (settings) :
![preview](../images/J19.png)


<br/>

* * * 

<br/>


## Jenkins executor :
* ***Executor*** will define , how many jobs run parallely at a time.
![preview](../images/J20.png)


<br/>

* * * 

<br/>



## Configure System 
* Go to Manage Jenkins >> Configure System 

![preview](../images/J24.png)
![preview](../images/J25.png)
![preview](../images/J26.png)
![preview](../images/J27.png)

<br/>

* * * 

<br/>

## Configure Global Security 
* Go to Manage Jenkins >> Configure Global Security 

![preview](../images/J24.png)
![preview](../images/J28.png)
![preview](../images/J29.png)

<br/>

* * * 

<br/>


## Manage Plugins :
* Plugins are a core feature of Jenkins, an open-source automation server used for continuous integration and continuous delivery (CI/CD) of software projects. Plugins allow users to extend the functionality of Jenkins by adding new features and integrations with other tools.

* Go to  Manage jenkins >> Manage Plugins
![preview](../images/J24.png)
![preview](../images/J30.png)
![preview](../images/J31.png)

* In the "Available" tab, you can browse for new plugins to install. You can use the search bar to find plugins by name, or you can browse through the list of available plugins.
* In the "Installed" tab, you can view all of the plugins that are currently installed on your Jenkins instance. You can also disable or uninstall plugins from this page.
* In the "Updates" tab, you can see if there are any updates available for the plugins you have installed. To update a plugin, select the checkbox next to the plugin and click on the "Download now and install after restart" button.
* In the "Advanced" tab, you can upload a plugin from your local machine or specify a custom update center URL.
***Note*** :  Some plugins may require a Jenkins restart to be fully installed or updated. When you install or update a plugin, Jenkins will 

<br/>

* * * 

<br/>


## Restart the jenkins :
* Multiple ways to restart 
  1. From ***cli*** from jenkins server : 
    ``` 
    sudo service jenkins restart     -- Restart Jenkins
    sudo service jenkins status      -- check the status of jenkins
    ```
    ![preview](../images/RJ.png)

  2. From ***GUI*** i,e Jenkins dashboard in browser: 
    ![preview](../images/J32.png)

  3. From  ***Manage Jenkins*** in Jenkins Dashboard
     ![preview](../images/J33.png)


<br/>
<br/>

* * * 

<br/>
<br/>