# EC2 (Elastic Compute Cloud) :
* An Amazon EC2 instance is a virtual server in Amazon's Elastic Compute Cloud (EC2) for running applications on the Amazon Web Services (AWS) infrastructure

## Create a EC2 in AWS :
* To create a EC2 in AWS , follow the below screenshots with instructions :
* Search of EC2 in AWS Dashboard 
* ***Note*** : When creating New keypair , a file will be downloaded(which requires when connecting to the server).
![preview](../images/E1.png)  
![preview](../images/E2.png) 
![preview](../images/E3.png) 
![preview](../images/E4.png) 
![preview](../images/E5.png) 

<br/>

* * * 

<br/>


## Connect to the EC2  / Disconnect from EC2 :  :
* To connect to the EC2 instance need a KeyPair file downloaded while creating the server.

1. Open the AWS dashboard get the command to connect to the EC2.
![preview](../images/E6.png) 
![preview](../images/E7.png) 

2. Open Mobaxterm and makesure the file downloaded while creating Keypair  is there in the present path . Paste the command copied from AWS dashboard
![preview](../img/ANS7.png) 
![preview](../images/E9.png) 

3. Disconnect from EC2 >> exit (or) Ctrl+ d :
![preview](../images/E10.png) 


<br/>

* * * 

<br/>

## Terminate EC2 in AWS : 
* To terminate/kill the EC2 in AWS , follow the screenshots with instructions:
   * **Terminate instance** : Permanent Delete/kill of instance 
   * **Stop instance**      : Temporary stopping , can start at anypoint in future
   * **Reboot instance**    : restart/reboot the instance 
   
![preview](../images/E11.png) 


<br/>

* * * 

<br/>


## Change ***Instance type*** of a EC2 :
* Changing Instance type is changing the size of the EC2 instance.

1. EC2 server has to be stopped to change the instance type:
![preview](../images/E12.png) 
![preview](../images/E13.png) 

2. Go to Actions >> Instance settings >> Change instance type 
![preview](../images/E14.png) 
![preview](../images/E15.png) 

3. Now you will have the server with changed **Instance type** >>  Start the Instance
![preview](../images/E16.png) 



<br/>

* * * 

<br/>


## Setting up Inbound rule to All Traffic for EC2 in AWS:
* Got to EC2 dashboaed >> check the server >> Security >> Inbound rules >> Security groups
![preview](../images/E17.png) 

* Edit the Inbound rules 
![preview](../images/E18.png) 
![preview](../images/E19.png) 
![preview](../images/E20.png) 
![preview](../images/E21.png) 



## Create a Centos EC2 in AWS :
* Creating centos is same like Ubuntu creation , the only difference is the Centos will be available in ***AWS Marketplace AMIs***
![preview](../img/C1.png)
![preview](../img/C6.png)
![preview](../img/C7.png)



* ***NOTE*** :- Select Centos from **Browse more AMIs** refer below steps

* Select Centos from ***Browse more AMIs*** :
![preview](../img/C2.png) 
![preview](../img/C3.png) 
![preview](../img/C4.png) 
![preview](../img/C5.png) 

