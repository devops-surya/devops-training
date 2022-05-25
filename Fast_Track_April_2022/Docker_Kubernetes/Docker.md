# Docker :

## The evolution of applications ( VM vs Containers):
 ![preview](../images/d1.png)

* Docker is an open source containerization platform. It enables developers to package applications into containers—standardized executable components combining application source code with the operating system (OS) libraries and dependencies required to run that code in any environmen
* Docker provides the ability to package and run the application in a loosely isolated environment called a  container. 
* Containerazation:  The procces of making your application run on the docker conatiners.
* Image : Docker image is a procees of packaging your application.
* For the docker documentation [REFER HERE](https://docs.docker.com/) 


## Understand Container :
* Every app running in container will be using the base os.
* Every container running in docker wil be having process id.
* Application running inside the container will have storage, CPU, RAM , network.
* Each container running in the docker is going to have ip address.

## Installing docker :
* Scripted way of installing docker [REFER HERE](https://get.docker.com/)
* Installing docker [REFER HERE](https://docs.docker.com/engine/install/ubuntu/)

## Dockerhub & Playground:
* Signup in dockerhub [REFER HERE](https://hub.docker.com/signup)
* Docker playground     
 ![preview](../images/dp1.png)
 ![preview](../images/dp2.png)
 ![preview](../images/dp3.png)
 ![preview](../images/dp4.png)


## Docker workflow :
  * Install docker which install two components :
   1. Docker Client
   2. Docker Daemon
  * When we use docker commands, docker client speaks with docker daemon to do the stuff
 ![preview](../images/Docker3.png)

## DockerHub:
* DockerHub is the default remote registry to the docker, where you can store images and use the images when required
* There are many private registries:
  * ECR - (Elastic container registry provided by AWS)
  * ACR - (Azure container regitry provided by Azure)

```sh
* List images in local :
docker image ls

* To run a sample helloworld container :
docker container run hello-world

* List container in local:
docker container ls -a
```
 ![preview](../images/docker143.png)

* Docker cheat sheet [REFER HERE](https://www.docker.com/wp-content/uploads/2022/03/docker-cheat-sheet.pdf)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## Container creation understanding :
* Write a Dockefile >> create image from Dockerfile >> create container from image
 ![preview](../images/dw.png)


## Basic Dockerfile syntax :
```
INSTRUCTIONS <ARGUMENTS>
```
* Some of the INSTRUCTIONS are FROM , RUN , CMD , ENTRYPOINT , ARG 

## Dockerfile for the java :
* Make folder of sample and create a Dockerfile in that samplefolder
```
mkdir sample 
cd sample
vi Dockerfile
```
* Search for the ubuntu image in the dockerhub . For latest image follow below
![preview](../images/h1.png)
* After adding Instructions and arguments , Dockerfile looks as below:
```
FROM ubuntu:latest
RUN  apt-get update
RUN  apt-get install openjdk-8-jdk -y
```

* To create a image from dockerfile follow below steps:
```
docker image build -t <imagename> .
docker image build -t <imagename> <pathtothedockerfile>
docker image build -t myfirstimage .

```

* Dockerfile is convention , we can also change the filename
![preview](../images/Docker7.png)
![preview](../images/Docker5.png)
![preview](../images/Docker6.png)

* To run the image we have created 
```
docker conatiner run <imagename>
docker conatiner run myfirstimage
docker conatiner ls 
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

## Installing docker :
 * Installing by script based :

```
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

``` 
![preview](../images/Docker9.png)

## RUN :
* This instructor executes your commands in the Dockerfile
* Every RUN instructor stores as a single layer .
* syntax :
```
RUN <command>
RUN ["executable, "param1", "param2" ]
```
* shell way of providing RUN command:
```
RUN echo sample
```
* exec way of providing RUN command
```
RUN ["echo", "sample"]
```


## ENTRYPOINT:
* This is the command thats executed when the container starting.
* syntax:
```
ENTRYPOINT [ "executable, "param1", "param2"  ]
ENTRYPOINT executable param1 param2 
```

## CMD :
* This will be excuted when the container starting , if the ENTRYPOINT is no there 
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

## Creating a Dockefile for SAMPLEWAR :
 * Install JAVA 
 * Install tomcat
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

## Dockerfile for the second approach:
```
FROM tomcat:8
LABEL author="surya"
ADD https://tomcat.apache.org/tomcat-7.0-doc/appdev/sample/sample.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD [ "catalina.sh", "run" ]
```
* Run the above Dockerfile wiht below commads
```
docker image build -t samplewar .
```
![preview](../images/Docker10.png)
![preview](../images/Docker11.png)
* To create a cotainer from the image of samplewar follow below steps:
```
docker container run samplewar
```

* To run the container on the detach mode follow below:
```
docker container  run -d samplewar
```
* To check the application ruuning on tomcat , we use -P to publish one of the port on the base OS to the container:
```
docker container -d  -P run samplewar
```
![preview](../images/Docker12.png)
![preview](../images/Docker13.png)


* To check the samplewar application accessible to the outside world:

```
ipaddress:<port>/sample
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

# Instructions:

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

## Example  Dockerfile with above Instructions

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

##  CMD &  ENTRYPOINT :
* These can be overwritten while creating a container:

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
## Commands:
```
docker container ls   ---- list of running container 
docker container ls -a    ---- list of all contaner running and exited
docker image ls         ----- list all the images

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

## Inspect an Image:
* Create a folder with java 

```
mkdir java 
cd java/
vi Dockerfile
```

```
FROM ubuntu:18.04
RUN apt-get update
RUN apt-get install openjdk-8-jdk -y
```

* Run the above Dockerfile :

```
docker image build -t java:1.0 .
docker image build -t java:2.0 .
```
* From one Dockerfile we can create multiple images.
* From one image we can also create multiple containers.

![preview](../images/Docker14.png)

## To inspect an image 
```
docker image inspect <imagename>
```

## To publish our own specified port :
```
docker conatiner run -d -p 8005:8080 <imagename>
```
![preview](../images/Docker15.png)

## Portforwarding:
* It is used to access our application running inside the container 

```
docker conatiner run -P <image>
docker conatiner run -p <hosport>:<conatinerport>
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
docker conatiner run -P <dockerimage>
```

## Detached mode:

* Docker conainer runs in the background .

```
docker conatiner run -d -P <imagename>
```

## Interactive :
* In interactive mode we can interact with docker using terminal (/bin/bash, /bin/sh)
* We will be using -it in the docker command
```
docker conatainer exec -it -P <imagename> /bin/bash 
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

## Adding name to the container :

```
docker container  run --name <nameofconainer>  -d -P <image>
```

![preview](../images/Docker15.png)

## Delete an image :

```
docker image rm <imagename>
docker image rm -f <imagename>
```
* To delete all images :

```
docker rmi $(docker images -a -q)
```

## To get into the container :

```
docker exec -it <conainername>/<containerid> /bin/bash
```
![preview](../images/Docker16.png)

## To delete the docker container :

```
docker container rm <conatinername>/<conatinerid>
docker container rm -f  <conatinername>/<conatinerid>
```
* For more info [REFERHERE](https://docs.docker.com/engine/reference/commandline/container_rm/)

## Namespaces:
![preview](../images/Docker18.png)

* As the containers are not reliable .That means the containers are going to stop/kill/died when there is no service running inside the container.
* When the containers are stopped the data inside the containers also lost.
* For the above isuue to be resolved , there is a concept of volumes, where we can attach the volumes. The volumes will be available even after the container is lost

## Volumes :
* volumes 
* Bind mount
* tmpfs

* For docker volumes [REFERHERE](https://docs.docker.com/storage/volumes/)

# DELETING/INSPECT/PRUNE volumes
* For Document [REFERHERE](https://docs.docker.com/engine/reference/commandline/volume_rm/)

```
docker volume rm <volumename>
docker volume rm  -f <volumename>
```
# CNM(Conatiner Networking Model)
* For Document [REFERHERE](https://docs.docker.com/network/)