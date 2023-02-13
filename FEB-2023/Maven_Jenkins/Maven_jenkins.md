# MAVEN & JENKINS


# Maven:
* Maven is a build automation tool and it helps DevOps in providing automation around the Build phase of the DevOps Life Cycle Management.

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
  * compile
  * Test
  * package
  * Install
  * clean
## compile: __mvn compile__
* Compile : - compile the source code
* when you  do  ```__mvn compile__```. It creates the  classfile.

## Test: *mvn test*
* test :- run unit tests

## package :  *mvn package*
* This will create the package (.war/.jar/.ear)

## clean :  *mvn clean*
* when you do clean , it will delete the old war and create the war.
* Basically the output will be stored in the target folder.

```
mvn test = mvn compile + mvn test
mvn package = mvn compile + mvn test + mvn package

```
<br/>

* * * 
<br/>


## pom.xml : 

* Developer defines the dependencies to build the project and also he will define the output of the build.
* POM stands for Project Object Model. It is the fundamental unit of work in the Maven. It is an XML file. It consists of all the information about the projects and the build configuration details used to build the project. It resides in the base directory of the Maven as the pom.xml
![preview](../images/jenkins40.png) 

<br/>

* * * 
<br/>


## Types of Maven repositories :  central, local, and remote

![preview](../images/mr.png)  

![preview](../images/jenkins38.png)

<br/>

* * * 
<br/>


## Build the code manually using maven:

* Clone the code from github.

```
git clone https://github.com/devops-surya/game-of-life.git
cd game-of-life.git
```
![preview](../images/jen21.png)  
![preview](../images/jen22.png)  

* ***mvn package***

![preview](../images/jen23.png)  
![preview](../images/jen24.png)  


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
* Jenkins is an open source continuous integration/continuous delivery and deployment (CI/CD) automation software DevOps tool written in the Java programming language. It is used to implement CI/CD workflows, called pipelines.
* Jenkins is a ci/cd tool
* ci -- continous integration 
* cd -- continous delivery / continous deployment

## Basic flow of devops :
![preview](../images/jenkins1.png)
![preview](../images/jenkins3.png)
![preview](../images/sqpipeline.png)
