
## To create a EKS cluster follow below steps :

1. Create a role with AmazonEKSClusterPolicy attached and call it as eksclusterrole

![preview](../img/EKS1.png)
![preview](../img/EKS2.png)
![preview](../img/EKS3.png)
![preview](../img/EKS4.png)
![preview](../img/EKS5.png)

2. Create a EKS cluster from the AWS console.

![preview](../img/EKS6.png)
![preview](../img/EKS7.png)
![preview](../img/EKS8.png)
![preview](../img/EKS9.png)
![preview](../img/EKS10.png)
![preview](../img/EKS11.png)
![preview](../img/EKS12.png)
![preview](../img/EKS13.png)
![preview](../img/EKS14.png)


3. Create a Ubuntu EC2 instance and install the Kubectl , IAM authenticator , aws cli 
    * Create a Ec2 ubuntu server :
      ![preview](../img/EKS15.png)
      ![preview](../img/EKS16.png)
      ![preview](../img/EKS17.png)
      ![preview](../img/EKS18.png)

    * Install kubectl -- [REFERHERE](https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html)

      ![preview](../img/EKS19.png)

    * Install IAM Authenticator -- [REFERHERE](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

      ![preview](../img/EKS20.png)

    * Install AWS CLI -- [REFERHERE](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html)

      ![preview](../img/EKS22.png)
      ![preview](../img/EKS21.png)
    


4. Create a IAM user with admin access in AWS  and configure the IAM user on  your K8S-Master instance by using aws-cli.
    * Create IAM user with Admin access :
      ![preview](../img/EKS23.png)
      ![preview](../img/EKS24.png)
      ![preview](../img/EKS25.png)
      ![preview](../img/EKS26.png)
      ![preview](../img/EKS27.png)
      ![preview](../img/EKS28.png)
      ![preview](../img/EKS29.png)
    * Configure IAM user to the K8s-Master to authenticate AWS: 

        ```
        aws configure 

        ```
      ![preview](../img/EKS30.png)

    * Run below command to get the config file downloaded to local , it helps us to connect to eks cluster.

      ```
      aws eks --region <region> update-kubeconfig --name <clustername>

      aws eks --region us-east-2 update-kubeconfig --name ekscluster

      ```
      ![preview](../img/EKS31.png)


* To check the kubectl configured correctly try the below command

```
kubectl get svc 
kubectl get nodes
```


5. Create a IAM role for EKS worker nodes with AmazonEKS_CNI_Policy , AmazonEKSWorkerNodePolicy, AmazonEc2ContainerRegistryReadOnly
![preview](../images/kub8.png)
![preview](../images/kub9.png)
![preview](../images/kub10.png)

6. Create/add a nodegroup to the cluster  from AWS console.
![preview](../images/kub11.png)
![preview](../images/kub12.png)
![preview](../images/kub13.png)
![preview](../images/kub14.png)
![preview](../images/kub15.png)




* For the sample twotire code deployment [REFERHERE](https://github.com/learnitguide/kubernetes-knote)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>