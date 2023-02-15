# MAVEN & JENKINS


# Maven:
* Maven is a build automation tool used primarily for Java projects.

## Build tools
   * c => Make, GCC
   * Java => Ant, Maven, Gradle
   * .net => MSBuild, dotnet build

## Install maven 

```
sudo apt update
sudo apt install maven
mvn -version
```
<br/>

* * * 
<br/>

## MAVEN GOALS:

* ***compile***: This goal compiles the source code of the project and creates the class files.

* ***test***: This goal runs the unit tests of the project.

* ***package***: This goal packages the compiled code and resources into a distributable format, such as a JAR, WAR, or ZIP file.

* ***install***: This goal installs the packaged artifact into the local repository, making it available for other projects to use.

* ***clean***: This goal removes all the generated files and directories created by the previous build.

* ***deploy***: This goal deploys the packaged artifact to a remote repository or a remote server.

```
mvn test = mvn compile + mvn test
mvn package = mvn compile + mvn test + mvn package
mvn clean package = mvn clean + mvn compile + mvn test + mvn package
```
<br/>

* * * 
<br/>

## Build the code manually using maven:

* Clone the code from github.

```
git clone https://github.com/devops-surya/SampleMavenProject.git
cd SampleMavenProject
```
![preview](../images/M1.png)  

* ***mvn package***

![preview](../images/M2.png)  
  
* ***mvn install***

![preview](../images/M3.png)  

* ***mvn clean install*** 
![preview](../images/M4.png)  


<br/>

* * * 
<br/>


## Types of Maven repositories :  Local, Central & Remote

![preview](../images/mr.png)  


* Maven supports three types of repositories:

    * **Local repository** : This is the local cache where Maven stores the downloaded artifacts on the developer's machine. By default, it's located in the .m2 directory in the user's home directory.

    * **Remote repository** : This is a network location, usually an HTTP or HTTPS URL, where Maven can download the required artifacts. Remote repositories can be public or private, and they can be hosted on a local network or on the internet.

    * **Central repository** : Maven comes with a default set of remote repositories, such as the Maven Central Repository and the JBoss Community Repository. However, you can also configure custom repositories in your POM file, either by specifying their URLs or by setting up a repository manager that can host and manage your custom repositories.

* ***NOTE***: When you add a dependency to your project's POM file, Maven first checks the local repository for the dependency. If it's not found, it then checks the remote repositories configured in the POM file. If the dependency is not found in any of the configured repositories, the build process fails with an error.


![preview](../images/LR.png)

<br/>

* * * 
<br/>


## pom.xml : 

* In Maven, the Project Object Model (POM) is an XML file called pom.xml that describes the project and its configuration. The POM file is located at the root of the project's directory and contains information about the project's name, version, dependencies, build process, and more.

![preview](../images/pom.png) 




<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>



# Jenkins:
* Jenkins is an open source __continuous integration/continuous delivery and deployment__ (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.
* Jenkins is a CI/CD tool
    * ***CI (Continous integration)*** : Continuous Integration is the practice of merging code changes into a shared repository frequently and automatically verifying that the resulting code builds, tests, and integrates successfully.
    * ***CD -- Continous Delivery / Continous Deployment*** :
        * **Continous Delivery** : Continuous Delivery is a software development practice that aims to make the release process more efficient and reliable by automating the entire software delivery pipeline. The idea is to ensure that code changes are always in a releasable state and can be deployed to production at any time. Continuous Delivery typically involves a continuous integration process that compiles and tests the code, followed by an automated deployment process that deploys the built artifacts to a staging environment. Once the code has been successfully tested in the staging environment, it can be promoted to the production environment.
        * **Continous Deployment** : Continuous Deployment, on the other hand, is a practice where every code change that passes the automated tests is automatically deployed to production. This means that any changes made to the code are automatically released to the users without any human intervention. Continuous Deployment is a more advanced version of Continuous Delivery and is generally suitable for organizations with high release frequency and the ability to handle fast feedback loops.

## Basic flow of devops :
![preview](../images/jenkins1.png)
![preview](../images/jenkins3.png)
![preview](../images/sqpipeline.png)
