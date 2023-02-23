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
![preview](../images/sqpipeline1.png)
![preview](../images/jenkins3.png)


<br/>

* * * 

<br/>

## Installing Jenkins 
* prerequisites:
1. Ubuntu
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
```
sudo apt-get update
sudo apt-get install openjdk-11-jdk

java -version

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt-get update
sudo apt-get install jenkins
```

* To open jenkins on brower 
* ***NOTE*** : jenkins runs on port of 8080 . So port 8080 must be opened in EC2 server (or) set inbound rule to All Traffic .
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



## Scenario-1: Create a CI Job.
### Find below requirements :
```
Need a Freestyle Job that should automatically detect the changes in github, get the code from SampleMavenProject, build it by using Maven &  Delete the Workspace for every build.
```
![preview](../images/SN-1.png)

![preview](../images/J13.png)
![preview](../images/J34.png)
![preview](../images/J35.png)
![preview](../images/J36.png)
![preview](../images/J37.png)

* Explore ***Console Output*** of **SMP** Job
![preview](../images/J38.png)
![preview](../images/J39.png)
![preview](../images/J40.png)
![preview](../images/J41.png)

<br/>
<br/>

* * * 

<br/>
<br/>

## Scenario-2: Add Post-build action to the Scenario-1 
### Find below requirement for Post-build actions:
```
Configure Scenario-1 CI job with **Archive the artifacts** & **Publish JUnit test result report** Post-build actions 
```
* ***Archive the artifacts*** -- It will provide option to download the artifact from the Jenkins Dashboard
* ***Publish JUnit test result report*** -- It will publish the test result in the Jenkins Dashboard 

![preview](../images/SN-2.png)


![preview](../images/J38.png)
![preview](../images/J42.png)
![preview](../images/J43.png)
![preview](../images/J44.png)
![preview](../images/J45.png)
![preview](../images/J46.png)
![preview](../images/J47.png)



<br/>
<br/>

* * * 

<br/>
<br/>

##  Understand the build process in Jenkins :

  * A ***build*** in Jenkins refers to the process of running a job, which typically involves compiling the source code, running tests, and producing artifacts etc. Each build in Jenkins is assigned a build number, which is incremented with each new build of a job. You can view the build history for a job in Jenkins, including the build number, the date and time of the build, and the status of the build (success or failure). You can also view the console output for a build, which shows the output of the build process, including any errors or warnings that occurred during the build.

  * The ***Jenkins workspace*** directory is typically a subdirectory of the ***Jenkins home directory*** and is unique to each job. When a job is triggered, Jenkins will create a new workspace directory for the job and copy the source code from your source control system into the workspace.




## Jenkins Home Directory Structure  :

  * In Jenkins, the ***home directory*** is the top-level directory where Jenkins stores all its configuration, plugins, and other related files. The location of the Jenkins home directory varies depending on the operating system and the installation method used.

  * When you install Jenkins on a Unix-like system, such as Linux or macOS, the default Jenkins home directory is usually located at /var/jenkins_home. On Windows, the default location is usually C:\Program Files (x86)\Jenkins.

![preview](../images/J48.png)
![preview](../images/J49.png)



  * The Jenkins home directory contains several important directories and files, including:

      * config.xml: This file contains the main configuration settings for Jenkins, such as security settings, system properties, and global tool installations.

      * jobs/: This directory contains the configuration and workspace directories for each Jenkins job. Each job is stored in a separate directory within the jobs/ directory.
      
      * jobs/**Jobname**/builds/: This directory contains all the build related information like no of builds and build history 
      
      * plugins/: This directory contains all the installed plugins for Jenkins. Each plugin is stored in a separate directory within the plugins/ directory.

      * secrets/: This directory contains sensitive information, such as passwords and API keys, that Jenkins uses for authentication and authorization.

    * users/: This directory contains the user accounts and their associated settings, including passwords and permissions.

It's important to back up the Jenkins home directory regularly, as it contains all the important configuration and data for your Jenkins installation. This will allow you to easily restore your Jenkins instance in case of a system failure or other issue.





<br/>

* * * 

<br/>


## Build with parameters:
  * In Jenkins, you can create a build job that accepts parameters from the user. This allows you to customize the build process and pass in values that are specific to the build.

      * String Parameter: Allows the user to enter a text value.

      * Boolean Parameter: Allows the user to select a checkbox.

      * Choice Parameter: Allows the user to select a value from a dropdown list.

      * File Parameter: Allows the user to upload a file.


### Official Dcoument for Parameters :
* Git parameter [ReferHere](https://plugins.jenkins.io/git-parameter/)
* String parameter [ReferHere](https://wiki.jenkins.io/display/JENKINS/Parameterized+Build)
* Choice Parameter [ReferHere](https://plugins.jenkins.io/extensible-choice-parameter/)
* Active choice parameter [ReferHere](https://plugins.jenkins.io/uno-choice/#:~:text=The%20Active%20Choices%20plugin%20is,or%20rich%20HTML%20UI%20widgets.)

![preview](../images/J50.png)



#### Scenario-3 : Install & Configure ***Git Parameter***  to pass the branch paramater while running the Job .
    
![preview](../images/SN-3.png)


  1. Install ***Git Paramter plugin*** 

![preview](../images/J24.png)
![preview](../images/J30.png)
![preview](../images/J31.png)
![preview](../images/J51.png)
![preview](../images/J52.png)
![preview](../images/J53.png)

  2. Configure ***Git Paramter plugin*** in the __SMP__ Jenkins Job

![preview](../images/J38.png)
![preview](../images/J54.png)
![preview](../images/J55.png)
![preview](../images/J56.png)
![preview](../images/J57.png)
![preview](../images/J58.png)



<br/>

* * * 

<br/>




### Scenario-4:  Create a NewJob SMP-2 , it should be copied from the existing SMP Job.
![preview](../images/SN-4.png)


* Copy/Clone the existing Job , will help us in this scenario.
* when you copy a job, it will inherit the settings and configuration of the original job, including the build history.


![preview](../images/J62.png)
![preview](../images/J63.png)
![preview](../images/J64.png)
![preview](../images/J65.png)
![preview](../images/J66.png)


<br/>

* * * 

<br/>

## Upstream and Downstream projects:

* In Jenkins, "upstream" jobs are those that trigger or initiate the execution of other jobs, while "downstream" jobs are those that are triggered or executed by upstream jobs.

![preview](../images/UD.png)


* For example, let's say you have two jobs, Job A and Job B, where Job A triggers Job B when it completes successfully. In this case, Job A is the upstream job and Job B is the downstream job.

  * Here are some examples of upstream and downstream jobs in Jenkins:

   * Upstream job: Build and package an application.
      * Downstream jobs: Deploy the application to a test environment, run automated tests on the application, deploy the application to a production environment.

   * Upstream job: Pull code changes from a source code repository.
      * Downstream job: Build and test the code changes, deploy the changes to a staging environment.

   * Upstream job: Run a performance test on an application.
      * Downstream job: Analyze the performance test results and provide recommendations for optimizing the application.

By defining upstream and downstream jobs in Jenkins, you can create complex workflows and ensure that all the necessary steps are executed in the correct order.

### Install ***Parameterized Trigger*** plugin :
* Parameterized Trigger is a plugin in Jenkins that allows you to trigger a downstream job with certain parameters from an upstream job. This plugin provides flexibility and customization by enabling you to pass variables and parameters from one job to another.
  
  * Go to **Manage Jenkins** >> **Manage Plugin**
![preview](../images/J59.png)
![preview](../images/J60.png)
![preview](../images/J61.png)



### Scenario-5: Configure the Upstream & Downstream as per below requirement :

```
1. Upstream Job : Build a ***SMP*** Job from Dev Branch
2. Downstream Job: Once the **SMP** Job is sucessfull , it has to build the Downstream Job(SMP-2) with Master Branch.
```
![preview](../images/SN-5.png)


* 1. Configure Upstream Job :
![preview](../images/J67.png)
![preview](../images/J68.png)
![preview](../images/J69.png)
![preview](../images/J70.png)

* 2. Build UpstreamJob with Dev branch it should trigger Downstream with master branch : 
![preview](../images/J71.png)
![preview](../images/J72.png)

    * Go to dashboard and check for the SMP-2 to trigger automatically :
![preview](../images/J73.png)

    * Go to Job __SMP-2__ >>  __Console Output__ and check for whether the Job triggered from Master branch :
![preview](../images/J74.png)



<br/>

* * * 

<br/>


## Jenkins Node/slave/Agent:
![preview](../images/JMS.png)

* In the context of the Jenkins, a "node" refers to a physical or virtual machine that is set up to perform build and testing tasks as part of a Jenkins job.

* A Jenkins node is also known as a "slave", as it operates as a worker machine that can be controlled by the Jenkins master server. A node can run on a variety of operating systems, including Linux, macOS, and Windows.

* In Jenkins, you can configure multiple nodes to distribute the build and testing workloads across a cluster of machines, which can help to improve performance and reduce the time required for building and testing your code. By setting up nodes, you can also run jobs in parallel, which can help to optimize resource utilization and speed up the overall build process.

* Nodes can be configured to have different sets of tools and plugins installed, which makes it possible to support multiple build environments. Once a node is set up and registered with the Jenkins master, you can assign Jenkins jobs to specific nodes, depending on the requirements of the job.


## Understanding Pipeline with Jenkins Node: 
![preview](../images/sqpipeline1.png)
![preview](../images/sqpipeline.png)


## Configure a Jenkins Node and attach it to the Jenkins Master:

![preview](../images/JA.png)

1. Configure the Jenkins Node :
    * Install ***Java*** on Jenkins Node :
    ```
    sudo apt-get update

    sudo apt-get install openjdk-8-jdk
    ```
    * Create a user in ***jenkins User*** in Jenkins Node & provide ***admin permissions***
    ```
    sudo su                  -- Change as root(Admin) user.
    adduser jenkins          -- create user 
    visudo                   -- Opens sudoers file

    ```
    * Enable ***PasswordAuthentication***
    ```
    vi /etc/ssh/sshd_config 
    
    ====
    PasswordAuthentication Yes
    ===

    sudo service sshd restart

    ```


* To add the node to the jenkins as per the above image. Do the ssh-keygen as shown below in jenkins-master:

```
ssh-keygen
ssh-copy-id username@ipaddress
```

![preview](../images/jenkins62.png)


* On node , do the below steps:

```

sudo su 

sudo apt-get update

sudo apt-get install openjdk-8-jdk

vi /etc/ssh/sshd_config 

PasswordAuthentication Yes

sudo service sshd restart

adduser jenkins

visudo -- add jenkins to the sudo group

```

## Add node/slave to the jenkins.

* In manage jenkins => mange nodes 

![preview](../images/jenkins63.png)

![preview](../images/jenkins64.png)

![preview](../images/jenkins66.png)

![preview](../images/jenkins65.png)


![preview](../images/jenkins67.png)

## Use node/slave in the jenkins job:

![preview](../images/jenkins68.png)

![preview](../images/jenkins69.png)

<br/>

* * * 

<br/>
