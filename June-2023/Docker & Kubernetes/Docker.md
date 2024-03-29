# Docker :

## Basic Devops Pipeline :
![preview](../img/BasePipeline.png)
![preview](../img/BasicDockerPipeline.png)



<br/>

* * * 

<br/>

## Docker :

* Docker is an open source containerization tool. It helps to package applications into containers—standardized executable components combining application source code with the operating system (OS) libraries and dependencies required to run that code in any environment.
* __Containerazation__:  The process of making your application run inside the docker containers. 
* For the docker documentation [REFER HERE](https://docs.docker.com/) 

<br/>

* * * 

<br/>

## VM vs Containers:

![preview](../images/d1.png)

![preview](../img/diff.png)


   * A VM is essentially an emulation of a complete computer system, including its hardware and operating system. It runs on top of a host operating system and provides a self-contained environment that behaves like a real computer. Each VM has its own virtual CPU, memory, disk, and network interfaces, which are isolated from other VMs running on the same physical machine. This allows multiple operating systems to run on a single physical server, enabling better resource utilization and scalability.

   * On the other hand, a container is a lightweight, standalone executable package that includes everything needed to run a piece of software, such as code, libraries, and dependencies, but shares the kernel of the host operating system with other containers. This means that multiple containers can run on the same physical machine, but each container appears as a separate process with its own isolated file system, network interfaces, and process space. Containers provide a more efficient and portable way to package and deploy applications, as they can be easily moved between different environments without modification.

* In summary, while a virtual machine provides a complete virtual environment, a container provides a lightweight, isolated environment for a specific application or service. The choice between the two depends on the specific use case and requirements of the application.


## Advantages of using docker over VM :
* Docker offers several advantages over virtual machines (VMs) for deploying and managing software applications. Some of these advantages include:

    * __Lightweight__: Docker containers are much more lightweight than virtual machines. While a virtual machine includes a complete operating system, including the kernel, Docker containers share the host operating system kernel and only include the application and its dependencies. This means that Docker containers are much smaller in size and faster to start up.

    * __Faster deployment__: Due to their smaller size and simpler architecture, Docker containers can be deployed much faster than virtual machines. In fact, Docker containers can be deployed in just a few seconds, whereas virtual machines typically take several minutes to start up.

    * __Portability__: Docker containers are highly portable and can run on any system that supports Docker. This makes it easy to move applications between development, test, and production environments, or to deploy applications across multiple cloud providers or data centers.

    * __Resource efficiency__: Because Docker containers share the host operating system kernel, they are much more resource-efficient than virtual machines. This means that you can run more Docker containers on a single host system than you could virtual machines, which can help to reduce infrastructure costs.

* Overall, Docker provides a lightweight, portable, and efficient way to deploy and manage software applications, making it an increasingly popular choice for modern application development and deployment.


## Understand Container :
* Every app running in container will be using the base os.
* Every container running in docker will be having process id.
* Application running inside the container will have storage, CPU, RAM , network.
* Each container running in the docker is going to have ip address.

<br/>

* * * 

<br/>

## Installing docker :
* Scripted way of installing docker [REFER HERE](https://get.docker.com/)
* Installing docker [REFER HERE](https://docs.docker.com/engine/install/ubuntu/)


<br/>

* * * 

<br/>


## Container creation understanding :
* Write a Dockefile >> create image from Dockerfile >> create container from image
 ![preview](../images/dw.png)


<br/>

* * * 

<br/>



## Dockerhub & Playground:
### Dockerhub :
* DockerHub is the default remote registry to the docker, where you can store images and use the images when required
* There are many private registries:
  * ECR - (Elastic container registry provided by AWS)
  * ACR - (Azure container regitry provided by Azure)
* Signup in dockerhub [REFER HERE](https://hub.docker.com/signup)

### Docker playground
* Docker playground     
 ![preview](../images/dp1.png)
 ![preview](../images/dp2.png)
 ![preview](../images/dp3.png)
 ![preview](../images/dp4.png)


<br/>

* * * 

<br/>



## Hello-world container creation : 
```sh
* List images in local :
docker image ls

* To run a sample helloworld container :
docker container run hello-world

* List container in local:
docker container ls -a
```
 ![preview](../images/docker143.png)

* Docker cheat sheet [REFER HERE](https://docs.docker.com/get-started/docker_cheatsheet.pdf)


<br/>

* * * 

<br/>

## Docker workflow :
  * While installing docker it installs two components :
   1. Docker Client
   2. Docker Daemon
  * When we use docker commands, docker client speaks with docker daemon to do the stuff
 ![preview](../images/Docker3.png)

<br/>

* * * 

<br/>

## Dockerfile syntax :
```
INSTRUCTIONS <ARGUMENTS>
INSTRUCTION-1 <ARGUMENT-1>
;
;
;
;
;
INSTRUCTION-n <ARGUMENTS-n>
```
* Some of the INSTRUCTIONS are FROM , RUN , CMD , ENTRYPOINT , ARG 


<br/>

* * * 

<br/>

## Dockerfile for the java image :
### Compare with java installation on VM : 
![preview](../img/DockerfilecreationcomaparisonwithVM.png)

* Make folder of sample and create a Dockerfile in that samplefolder
```
mkdir sample 
cd sample
vi Dockerfile
```
* Search for the ubuntu image in the dockerhub . For base image follow below : 
![preview](../images/h1.png)

## FROM :
* This instructor is used to get the base image for your image creation .
* Syntax:

```
FROM <baseimagename>
```

* Example :
```
FROM Ubuntu:22.04
```


## RUN :
* This instructor executes your bash/linux commands in the Dockerfile
* Every RUN instructor stores as a single layer .
* syntax :
```
RUN <command>
RUN ["executable, "param1", "param2" ]
```
### shell way of providing RUN command:
```
RUN echo sample
```
### exec way of providing RUN command
```
RUN ["echo", "sample"]
```

* After adding Instructions and arguments , Dockerfile looks as below:

```
FROM ubuntu:22.04
RUN apt-get update  -y \
  && apt-get install openjdk-11-jdk -y
```

* To create a image from dockerfile follow below steps:
```
docker image build -t <imagename> .
docker image build -t <imagename> <pathtothedockerfile>
docker image build -t myfirstimage .

```

* Dockerfile is convention , we can also change the filename
![preview](../images/Docker5.png)
![preview](../images/Docker6.png)

* To create a container from the  image we have created 
```
docker container run <imagename>
docker container run myfirstimage
docker container ls 
docker container ls -a
```
![preview](../images/Docker8.png)





<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>


## Exercise: Install docker on EC2:
 * Scripted way of installing docker [REFER HERE](https://get.docker.com/)
 * Create a EC2 instance in AWS and run the below commands to install docker :

```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

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

## Instructors discussion image :
![preview](../img/Instructorsdiscussion.png)

## ENTRYPOINT:
* This is the instructor thats executed when the container creation.
* syntax:
```
ENTRYPOINT [ "executable, "param1", "param2"  ]
ENTRYPOINT executable param1 param2 
```

## CMD :
* This will be excuted when the container creation . If the ENTRYPOINT is not there , CMD is high priority.
* syntax:
```
CMD [ "executable, "param1", "param2"  ]
CMD executable param1 param2 
```

* If both the CMD and ENTRYPOINT exists, then the ENTRYPOINT will be excuted 

## EXPOSE :
* This intsructor is used to expose your port on the container 
* syntax:
```
EXPOSE <port>
EXPOSE 8080
```

## LABEL :
* This instructor adds metadata to your image :
* syntax:
```
LABEL <key>=<value>
LABEL author="myself"
LABEL project="myproject"
LABEL version="1.0"
```

## ADD and COPY :
* The two instructors are used to copy the files to the docker image.
* ADD instructor is uded to copying files from url and local machine.
* COPY instructor supports copying the files on the local machine.

* synatx:
```
ADD <src> <dest>
ADD <url> <dest>
COPY <src> <dest>
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

## Run container in multiplemodes :

## Attached mode:
* The container runs on foreground
* Default mode of docker

```
docker conatiner run  <dockerimage>
docker container run tomcat
```
![preview](../img/am.png)


## Detached mode:

* Docker conainer runs in the background .

```
docker conatiner run -d <imagename>
docker container run -d tomcat 
```

![preview](../img/dm.png)


## Interactive :
* In interactive mode we can interact with docker using terminal (/bin/bash, /bin/sh)
* We will be using -it in the docker command
```
docker container exec -it  <containerid/container name> /bin/bash 
```
## To get into the container :

```
docker container exec -it <conainername>/<containerid> /bin/bash
```
![preview](../img/im.png)


<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## Portforwarding:
* It is used to access our application running inside the container 
![preview](../img/pf.png)
![preview](../img/pf1.png)

```
docker container run -P <image>
```

## To publish on our own specified port :
```
docker container run  -p <hosport>:<conatinerport> <imagename>

docker container run -p 8005:8080 <imagename>
```
![preview](../img/pf2.png)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## Install docker on AWS EC2 server:
 * Scripted way of installing docker [REFER HERE](https://get.docker.com/)
 * Create a EC2 instance in AWS and run the below commands to install docker :

```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```
![preview](../img/di1.png)
![preview](../img/di2.png)
![preview](../img/di3.png)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## SAMPLEWAR Application deployment Using Docker in AWS EC2 server:


 ![preview](../img/BasicDockerPipeline.png)

 ![preview](../img/SampleDockerDeployment.png)



 * Install JAVA 
 * Install Tomcat
 * Downloading the war file and copying it to tomcat webapps
 * start the tomcat


### First approach :
  1. Taking baseimage of ubuntu  ---- FROM 
  2. Installing java     ----  RUN 
  3. Installing tomcat   ----  RUN 
  4. know the exact path of webapps 
  5. downloading the war file  and copy to the webapps -----  ADD/COPY
  6. Open port of tomcat on container   --- EXPOSE 
  7. starting the tomcat  ----  ENTRYPOINT/CMD

### Second approch:
  1. Taking the baseimage of tomcat directly --- FROM
  2. Downloading the war file and copying it to tomcat webapps --- ADD/COPY
  3. Open port of tomcat on container   --- EXPOSE 
  4. starting the tomcat  ----  ENTRYPOINT/CMD
  

### Dockerfile for the second approach:

```
FROM tomcat:8
LABEL author="surya"
ADD https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD [ "catalina.sh", "run" ]
```
* Run the above Dockerfile with below commands
```
docker image build -t samplewar .
```
![preview](../images/Docker10.png)
![preview](../images/Docker11.png)

* To create a container from the image of samplewar follow below steps:
```
docker container run samplewar
```

* To run the container on the detach mode follow below:
```
docker container  run -d samplewar
```


* To check the application ruuning on tomcat , we use -P to publish one of the port on the base OS to the container:
```
docker container run  -d  -P run samplewar
```
![preview](../img/di5.png)


* To check the samplewar application accessible to the outside world:

```
ipaddress:<port>/sample
```
![preview](../img/di4.png)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>


## Add name to the container :

```
docker container  run --name <nameofconainer>  -d -P <image>
```

![preview](../images/Docker15.png)
![preview](../images/Docker16.png)



## To inspect an image : 
* Docker inspect provides detailed information on constructs controlled by Docker. By default, docker inspect will render results in a JSON array.
```
docker image inspect <imagename>
```
![preview](../images/ins.png)

## Delete an image :

```
docker image rm <imagename>
docker image rm -f <imagename>
```
* To delete all images :

```
docker rmi $(docker images -a -q)
```


## To delete the docker container :

```
docker container rm <conatinername>/<conatinerid>
docker container rm -f  <conatinername>/<conatinerid>
```
* For more info [REFERHERE](https://docs.docker.com/engine/reference/commandline/container_rm/)


<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>


# Instructions:
![preview](../img/DockerInstructions.png)


## USER :
* This sets the username for any subsequent commands running by RUN , CMD , ENTRYPOINT
* syntax:
```
USER <username>
USER devops
```

## WORKDIR:
* This intruction sets the working directory for any subsequent commands running by RUN , CMD , ENTRYPOINT
* Syntax:
```
WORKDIR /home/devops/mypath
```

## ARG :
* This insruction allows variable to be passed while building image.
* syntax:
```
ARG <key>=<value>
```

## ENV:
* This insruction allows you to set the environmental variables for the docker image.
* syntax:
```
ENV <key>=<value>
```
* Environmental variable can also be replaced while container running.

## Example Dockerfile with above Instructions

```
FROM tomcat:8
LABEL author="surya"
USER devops
ARG url=https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war
ADD $url /usr/local/tomcat/webapps/
EXPOSE 8080
WORKDIR /home/devops/
ENV tomcatversion=8
CMD [ "catalina.sh", "run" ]
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

##  CMD &  ENTRYPOINT override :

* These can be overwritten while creating a container:
![preview](../img/DockerOverwrite.png)


```
docker container run -d samplewar echo hello
docker container run -d samplewar --entrypoint 
```

## stop/start pause/unpause

```
docker container stop <container-id>/<containername>
docker container start  <container-id>/<containername>
docker container pause  <container-id>/<containername>
docker container unpause  <container-id>/<containername>
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





