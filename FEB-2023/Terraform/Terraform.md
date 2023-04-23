# Terraform

* __Terraform__  is an open-source infrastructure as code (IaC) tool that enables you to define, provision, and manage your infrastructure resources across different cloud providers and platforms in a declarative and repeatable way.
![preview](../images/tf1.png)


## Prerequisites:
* Need to create a AWS free tier account.


## Need for Infrastructure Provisioning:
* The main moto of IAAC is that you write & execute the code to define, deploy, update and destroy your infrastructure.
* In CI/CD pipelines, we need to create various test environments according to organizational QA policy, and need to destroy them once after the work is done.


## Understanding of Terraform/Terminology:
* Terraform is a __infraprovisoning__ tool.
* __Infraprovisoning__ --- What ever you want to create for your project in the cloud is called as infraprovisoning.

![preview](../images/tf1.png)

* Any cloud we are using in terraform is called  as __Provider__.
* Whatever you want to create in the terrafrom is called as __Resource__.
* __Arguments__ are the inputs to your resource and __Attributes__ are outputs of your resources
* Terraform uses the __configuration language__ to write the terraform script.
* Terraform work on the multiple clouds.
* Terraform supported clouds [REFER HERE](https://registry.terraform.io/browse/providers)


<br/>

* * * 

<br/>


## Install Terraform:

* Terraform official document for installation - [REFERHERE](https://phoenixnap.com/kb/how-to-install-terraform)
* On windows : 

```sh
choco install terraform
```
* On ubuntu:

```sh
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform
```
* To check terraform version

```sh
terraform --version
```

<br/>

* * * 

<br/>


## Authenticate Terraform to speak with AWS: 
* Terraform speak to AWS by using IAM(Identity Access Management) user.
![preview](../img/TF1.png)
![preview](../img/TF2.png)
![preview](../img/TF3.png)
![preview](../img/TF4.png)
![preview](../img/TF5.png)
![preview](../img/TF6.png)
![preview](../img/TF7.png)
![preview](../img/TF8.png)
![preview](../img/TF9.png)
![preview](../img/TF15.png)
![preview](../img/TF10.png)
![preview](../img/TF11.png)


<br/>

* * * 

<br/>

## Install Terraform on ubuntu:
* create a EC2 server in AWS -- [REFERHERE](https://github.com/devops-surya/devops-training/blob/main/FEB-2023/EC2/EC2.md)

* Run the following command on EC2 :

```sh
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

```

* To check terraform version

```sh
terraform --version
```
![preview](../img/TF12.png)

<br/>

* * * 

<br/>

# Terraform syntax/Template for configuration language : 

## Provider syntax : [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

* In Terraform, a provider is a plugin that defines how to interact with a specific infrastructure platform, such as AWS, Azure, Google Cloud, or VMware. Each provider has its own set of resources and configuration options.

* Provider  syntax :

```sh
provider '<name>' {
    <arg1> = <value1>
    <arg2> = <value2>
}
```
* AWS provider terraform template [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

```sh
provider "aws" {
  region     = "ap-northeast-1"
  access_key = "AKIASAK53KCFRR4WX7OP"
  secret_key = "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"
}
```

<br/>

* * * 

<br/>

## Resource syntax : [REFERHERE](https://developer.hashicorp.com/terraform/language/resources/syntax)

* In Terraform, a resource represents an infrastructure object that you want to manage, such as an AWS EC2 instance, storage etc..

```
resource "<resource-type>" "<resource-name>" {
    arg1 = "value1"
      ...
      ..
      argn = "value2"

}
```

<br/>

* * * 

<br/>

## Agruments and Attributes:

* In Terraform, an argument is a value that is passed to a resource or module to configure its behavior. Arguments can be mandatory or optional, and they have specific names that correspond to the parameters of the resource or module.

* Attributes are values that can be retrieved from a resource or module after it has been created. 

![preview](../images/tf9.png)


<br/>

* * * 

<br/>


## Terraform template for AWS provider :

* AWS provider terraform template [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)


* Create a folder named ```terraformprovider``` 

```sh
mkdir terraformprovider
cd terraformprovider
```
* Create a file named ```provider.tf``` and add below content : 

```sh
provider "aws" {
  region     = "ap-northeast-1"
  access_key = "AKIASAK53KCFRR4WX7OP"
  secret_key = "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"
}

```
![preview](../img/TF13.png)


* T erraform initialize  :

```sh
terraform init 
```
* Terraform validate :

```sh
terraform validate . 
```

![preview](../img/TF14.png)




## AWS VPC & Subnet:
* Amazon __Virtual Private Cloud__ (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined.
* A __subnet__ is a segmented piece of a larger network. More specifically, subnets are a logical partition of an IP network into multiple, smaller network segments.

### Create VPC & Subnet from AWS console as below :
* __VPC Creation__ :
![Preview](../images/vpc1.png)
![Preview](../images/vpc2.png)
![Preview](../images/vpc3.png)
![Preview](../images/vpc4.png)

* __Subnet creation__ :
![Preview](../images/sn1.png)
![Preview](../images/sn2.png)
![Preview](../images/sn3.png)


###  Terraform template to  create VPC & Subnet in AWS:
* Create in file with extension __.tf__ (vpc-subnet.tf) in the folder of terraforsample
```
mkdir terraformsample
cd terraformsample
vi vpc-subnet.tf
```
* __Resource:aws_vpc__  --  [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)
* __Resource:aws_subnet__  --   [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet)

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPRSG3D6S3"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "myfirstsubnet"
  }
}

```

* To initialize provider plugins follow below:
```sh
terraform init  
```
![preview](../images/tf2.png)

* To validate to validate your script:

```sh
terraform validate 
```
![preview](../images/tf3.png)

* To run the terraform script 

```sh
terraform apply 
```

* To destroy the resource :

```sh
terraform destroy 
```


 
## Create a VPC/Subnet using multi files in the Terraform template :
* Create a folder  multifile
```sh
mkdir multiplefile
cd multiplefile
```
* Create a file __provider.tf__  and add below data to it:

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPRSG3D6S3"
  secret_key = "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"
}

```

* Create a file vpc.tf and add below content:
* __Resource:aws_vpc__  -- [REFERHER](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)

```sh
resource "aws_vpc" "myfirstvpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

```
* Create a file subnet.tf and add below data:
* __Resource:aws_subnet__  --   [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/subnet)
```sh
resource "aws_subnet" "myfirstsubnet" {
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "myfirstsubnet"
  }
}

```

* Run the below commands:
```sh
terraform init 
terraform validate 
terraform apply 
terraform destroy 
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

## Variables in terraform :
* In Terraform, variables are used to define values that can be passed into modules or configurations. These variables can be used to define values for things like IP addresses, instance types, or other parameters that are used in your infrastructure.

* There are several types of variables in Terraform:
    * Terraform variables [REFERHERE](https://www.terraform.io/language/values/variables)

    * String Variables: These variables are used to define strings of text, and can be defined using the string type.

    * Number Variables: These variables are used to define numerical values, and can be defined using the number type.

    * Boolean Variables: These variables are used to define true/false values, and can be defined using the bool type.

    * List Variables: These variables are used to define a list of values, and can be defined using the list type.

    * Map Variables: These variables are used to define a set of key/value pairs, and can be defined using the map type.


## SCENARIO-1:- Use variables & create multiple subnets:
1. First case : 

### vars.tf:
```sh
variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = string
  default = "10.0.1.0/24"
}
variable "subnetcidr1" {
  type = string
  default = "10.0.2.0/24"
}
variable "subnetcidr2" {
  type = string
  default = "10.0.3.0/24"
}

```

* The main.tf and vars.tf looks like below:
### main.tf
```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHP6XQQOREN"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr

  tags = {
    Name = "myfirstsubnet"
  }
}

resource "aws_subnet" "myfirstsubnet1" {
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr1

  tags = {
    Name = "myfirstsubnet1"
  }
}

resource "aws_subnet" "myfirstsubnet2" {
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr2

  tags = {
    Name = "myfirstsubnet2"
  }
}


```

* Run the below commands after the above data is replicated:

```sh
terraform init 
terraform validate 
terraform apply 
terraform destroy 
```

<br/>

* * * 

<br/>


## Count in terraform:
* count is a meta-argument defined by the Terraform language. It can be used with modules and with every resource type.
* __count.index__ — The distinct index number (starting with 0) corresponding to this instance.
* __count & count.index__ -- [REFERHERE](https://www.terraform.io/language/meta-arguments/count)

* __Example scrpt__ : The below script will fail stating conflicts in subnets CIDR .
```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "UH9kONWx18mKXQq9fCu03rJttvqhi1HzKYkoWBjP"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}
resource "aws_subnet" "myfirstsubnet" {
  count = 3 ## Create three similar subnets
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = "10.0.1.0/24"

  tags = {
    Name = "myfirstsubnet"
  }
}
```


### Using Count to create a VPC with multiple subnets(Note: Use list(string) in variable) 
* The main.tf and vars.tf look like below in the second case:

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = 3
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
}

=======================

variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = list(string)
  default = [ "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24" ]
}
```


<br/>

* * * 

<br/>


## length in terraform:
* __length__ determines the length of a given list, map, or string
* __length__ -- [REFER HERE](https://www.terraform.io/language/functions/length)
```
> length([])
0
> length(["a", "b"])
2
> length({"a" = "b"})
1
> length("hello")
5
```



### Use the length in terraform script then main.tf will change as below:

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = length(var.subnetcidr)
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
}

=======================

variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = list(string)
  default = [ "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24" ]
}
```



<br/>

* * * 

<br/>


## Depends_on:
* Use the depends_on meta-argument to handle hidden resource or module dependencies that Terraform can't automatically infer.
* __Dependson__ [REFER HERE](https://www.terraform.io/language/meta-arguments/depends_on)

### Use depends_on in terraform script , the main.tf looks as below:

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = length(var.subnetcidr)
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
  depends_on = [aws_vpc.myfirstvpc]
}

```



<br/>

* * * 

<br/>



## Security group:
* A security group is like a virtual firewall. It works much like a traditional firewall does. It consists of a set of rules that can be used to monitor and filter an instance's incoming and outgoing traffic in a Virtual Private Cloud (VPC) instance. Filtering is done on the basis of protocols and ports.

### Create a SecurityGroup in AWS console as shown below :
* __SecutityGroup Creation__ :
![preview](../images/sg1.png)
![preview](../images/sg2.png)
![preview](../images/sg3.png)
![preview](../images/sg4.png)

### Use __SecurityGroup__ in terraform script , the main.tf looks as below:
* __Resource: aws_security_group__  --   [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)

* After adding SG the main.tf look as below:
```sh
provider "aws" {
  region     = "ap-northeast-1"
  access_key = "AKIASAK53KCF5BH7UJRC"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}


resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id


  ingress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
  }

  egress {
    from_port        = 0
    to_port          = 0
    protocol         = "-1"
    cidr_blocks      = ["0.0.0.0/0"]
  }
  tags = {
    Name = "mySG"
  }
  depends_on = [aws_vpc.myfirstvpc]
}
```
### Create inbound/outbound rules to the securitygroup
* __Resource: aws_security_group_rule__ [REFER HERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule)
* Ingress is for creating the inbound rule and Egress is for creating the outbound rules.
* After adding the egrees in the terraform template it lokks as below:
```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}


resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id
  tags = {
    Name = "mySG"
  }
  depends_on = [aws_vpc.myfirstvpc]
}

resource "aws_security_group_rule" "alltraffic" {
  type              = "ingress"
  from_port        = 0
  to_port          = 0
  protocol         = "-1"
  cidr_blocks      = ["0.0.0.0/0"]
  security_group_id = aws_security_group.mySG.id
}

```


<br/>

* * * 

<br/>



## S3 in AWS :
* Amazon Simple Storage Service (S3) is a popular cloud storage service part of the Amazon Web Services (AWS). Amazon S3 cloud storage provides high reliability, flexibility, scalability and accessibility. The number of objects and the amount of data stored in Amazon S3 is unlimited.

### Create a S3 bucket in AWS console as shown below :
* __S3 Bucket creation__ :
![preview](../images/s31.png)
![preview](../images/s32.png)
![preview](../images/s33.png)
![preview](../images/s34.png)


### Terraform template to create s3 bucket:
* __Resource: aws_s3_bucket__  [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)
```sh
provider "aws" {
  region     = "ap-northeast-1"
  access_key = "AKIAYZCYFVHPSMCGSJPD"
  secret_key = "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"
}
resource "aws_s3_bucket" "myfirstbucket" {
  bucket = "my-first-test-bucket"

  tags = {
    Name        = "myfirstbucket"
  }
}

```


<br/>

* * * 

<br/>


## Data sources :
* Data sources are used to query the aws resources which are already created.
* Data sources allow data to be fetched or computed for use elsewhere in Terraform configuration.
### Create a subnet to  vpc, which is already created in aws.

```sh
provider "aws" {
  region     = "us-east-1"
  access_key = "AKIA3IUVW2N67JAQ2ZIA"
  secret_key = "CiVcsgEOQ5+HFmhqpBbUlatetc7nLl+WJeQ0BhGj"
}


data "aws_vpc" "selected" {
  id = "vpc-072fe7e68bab3c199"
}

resource "aws_subnet" "example" {
  vpc_id            = data.aws_vpc.selected.id
  availability_zone = "us-west-2a"
  cidr_block        = "10.0.0.0/24"
}
```


<br/>

* * * 

<br/>


## Terraform statefile :
* Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures. This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment.

![preview](../images/tfs.png)


<br/>

* * * 

<br/>


## Terraform plan : 
* Terraform plan create a plan-file , to create resources need to use the plan-file.
```
terraform plan -out mutilfile.plan
terraform apply mutilfile.plan
```

![preview](../images/tf10.png)
![preview](../images/tf11.png)

<br/>

* * * 

<br/>

## Target in terraform :
* Terraform allows you to target specific resources when you plan, apply, or destroy your infrastructure. 
* __Target__ : - [REFERHERE](https://learn.hashicorp.com/tutorials/terraform/resource-targeting)
### __syntax__ :
```
terraform apply/destroy -target="RESOURCE_TYPE.RESOURCE_NAME"

```
<br/>

* * * 

<br/>

## Terraform Registry 
* Terraform registry is a place where you can find the predefined modules(terrafrom scripts).
![preview](../images/tf14.png)

* __Module Document__ : - [REFER HERE](https://www.terraform.io/language/modules/syntax) 

### Using the module :
* VPC module -- [REFERHERE](https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws/latest)
* Usage of module : -  change the values from below Usage
![preview](../images/ft1.png)
* Use the below script to use the terraform module from registry :

```
provider "aws" {
  region     = "ap-northeast-1"
  access_key = "AKIASAK53KCFXPJBKMQ4"
  secret_key = "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"
}

module "vpc" {
  source = "terraform-aws-modules/vpc/aws"

  name = "my-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["ap-northeast-1a", "ap-northeast-1a", "ap-northeast-1a"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway = true
  enable_vpn_gateway = true

  tags = {
    Terraform = "true"
    Environment = "dev"
  }
}
```
<br/>

* * * 

<br/>

## Difference between terraform module and standard terrafrom template 

* In Terraform, a module is a collection of Terraform resources that are grouped together and managed as a single entity. A module can be thought of as a reusable package of Terraform code that can be used to create and manage a specific set of infrastructure resources. A module can be shared and reused across multiple Terraform configurations, making it easier to manage and maintain infrastructure code.

* On the other hand, a Terraform template is a single file that defines a set of resources to be created and managed by Terraform. It is a standard way of defining infrastructure-as-code using the Terraform language.

* The main difference between a Terraform module and a standard Terraform template is the level of abstraction and reusability. A Terraform template is a single file that defines the resources to be created and managed by Terraform, whereas a module is a collection of resources that can be reused across multiple Terraform configurations.

<br/>

* * * 

<br/>

### Creating a module : 
* Create a folder of samplemodule
```sh
mkdir samplemodule
cd samplemodule
```
* create a file of main.tf and add the below content:

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPVJGZVTSA"
  secret_key = "JHYKCFHb0328MHekUtSB//VxQthwzUfQtiVy78Tn"
}
module "singlefile" {
  source = "./singlefile"
  vpccidr = "10.0.0.0/16"
}

```
* Create a singlefile folder and add below content 
```
cd samplemodule
mkdir singlefile
```

```sh
main.tf:
======
resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = length(var.subnetcidr)
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
  depends_on = [aws_vpc.myfirstvpc]
}

resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
  tags = {
    Name = "mySG"
  }
  depends_on = [aws_subnet.myfirstsubnet]
}


vars.tf:
=======
variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = list(string)
  default = [ "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24", "10.0.4.0/24" ]
}

```
* After creating the module content , run the below command:

```sh
terraform init 
terraform validate
terraform apply 
```
![preview](../images/tf15.png)


<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## Complete VPC setup for an application:

![preview](../img/VPCsetup.png)

#### In AWS, you can create an Internet Gateway and attach it to your VPC to enable communication between your VPC and the Internet. An Internet Gateway is a logical entity that represents the AWS side of the connection. You can use it to communicate with resources outside of your VPC and allow outside resources to communicate with resources in your VPC.

#### A NAT Gateway is a highly available AWS-managed service that allows resources in a private subnet to connect to the Internet or other AWS services, without exposing those resources to the public Internet. NAT (Network Address Translation) Gateway translates the private IP addresses of instances in the private subnet to a public IP address when those instances communicate with the Internet or other AWS services.

### VPC Setup steps :
1. Create a VPC: To create a VPC, navigate to the AWS Management Console, select VPC from the Services menu, and click Create VPC. You'll need to specify a name, CIDR block, and any optional settings.

2. Create subnets: Once your VPC is created, you can create subnets by navigating to the Subnets tab in the VPC dashboard and clicking Create Subnet. You'll need to specify a name, CIDR block, and which Availability Zone you want the subnet to be in.

3. Create an internet gateway: An internet gateway (IG) allows traffic to flow between your VPC and the internet. To create an IG, navigate to the Internet Gateways tab in the VPC dashboard and click Create Internet Gateway.

4. Attach IG to VPC: To attach the IG to your VPC, select the IG in the dashboard and click Attach to VPC. Select your VPC from the dropdown menu and click Attach.

5. Create NAT gateway: If you want your instances in private subnets to access the internet, you'll need to create a NAT gateway. To create a NAT gateway, navigate to the NAT Gateways tab in the VPC dashboard and click Create NAT Gateway.

6. Create public and private route tables: You'll need to create two route tables - one for public subnets and one for private subnets. Navigate to the Route Tables tab in the VPC dashboard and click Create Route Table. Name your route table and select your VPC. Then click Create.

7. Associate subnets with route tables: Once you have created your route tables, you'll need to associate them with the appropriate subnets. To do this, select the route table in the dashboard and click the Subnet Associations tab. Click Edit and select the subnets you want to associate with the route table.

8. Configure routes: To allow traffic to flow between your VPC and the internet, you'll need to configure routes. In the public route table dashboard, click Edit routes and add a new route to your IG. For the private route table, add a new route to your NAT gateway.

9. Create security groups: Security groups act as a virtual firewall for your instances. To create a security group, navigate to the Security Groups tab in the VPC dashboard and click Create Security Group. Name your security group, select your VPC, and configure inbound and outbound rules as needed.

10. Launch instances: Now you can launch instances in your public and private subnets. Make sure to select the appropriate security group and subnet for each instance.




## EC2 instances creation in a customised VPC, subnet, SG, keyname : 
### Create ec2 from AWS console: 
* AMI , instancetype , no of instances , vpc , subnet , autoassign publicip , tags , SG , keyname should be used as shown in below images:
![preview](../images/ec1.png)
![preview](../images/ec2.png)
![preview](../images/ec5.png)
![preview](../images/ec3.png)
![preview](../images/ec4.png)
![preview](../images/ec6.png)
![preview](../images/ec7.png)
![preview](../images/ec8.png)
![preview](../images/ec9.png)
![preview](../images/ec10.png)
![preview](../images/ec11.png)

<br/>

* * * 

<br/>

### Terraform template to create ec2:
*  vars.tf and main.tf look like below:
```sh
vars.tf:
=======
variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = list(string)
  default = [ "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24", "10.0.4.0/24" ]
}

main.tf:
==========
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPQZCE4Z6P"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = length(var.subnetcidr)
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
  depends_on = [aws_vpc.myfirstvpc]
}

resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }


  tags = {
    Name = "mySG"
  }
  depends_on = [aws_subnet.myfirstsubnet]
}

resource "aws_instance" "myec2" {
  ami           = "ami-0cb4e786f15603b0d"
  instance_type = "t2.micro"
  key_name = "devops-training"
  vpc_security_group_ids = [ aws_security_group.mySG.id ]
  subnet_id = aws_subnet.myfirstsubnet[0].id

  tags = {
    Name = "myec2"
  }
  depends_on = [aws_security_group.mySG]

}

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

## Provisioners in terrafrom 
* Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction. Provisioners can also be  configuration management, etc..
* __Terraform Provisioners__ -- [REFERHERE](https://www.terraform.io/language/resources/provisioners/syntax)

## File provisioner:
```sh
provisioner "file" {
  source      = "conf/myapp.conf"
  destination = "/etc/myapp.conf"
```

## remote-exec:

```sh
  provisioner "remote-exec" {
    inline = [
      "sudo apt-get update -y ",
      "sudo apt-get install python -y"
    ]
  }
}
```

## Terraform provisioning :
* You are assigned with task of creating a VM and installing the necessary softwares the VM.
* Steps to be followed :
  1. Create a VM 
  2. Connection to the VM -- [REFERHERE](https://www.terraform.io/language/resources/provisioners/connection)
  ![preview](../images/c1.png)
  3. Installing necessary softwares by using provisioners.


* The terraform template look like below , if we use the provisioners:
```sh
vars.tf:
======
variable "vpccidr" {
  type = string
  default = "10.0.0.0/16"
}
variable "subnetcidr" {
  type = list(string)
  default = [ "10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24", "10.0.4.0/24" ]
}


main.tf:
=======
provider "aws" {
  region     = "us-west-2"
  access_key = "AKIATDL7EYHPSRBBULQD"
  secret_key = "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"
}

resource "aws_vpc" "myfirstvpc" {
  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc"
  }
}

resource "aws_subnet" "myfirstsubnet" {
  count = length(var.subnetcidr)
  vpc_id     = aws_vpc.myfirstvpc.id
  cidr_block = var.subnetcidr[count.index]

  tags = {
    Name = "myfirstsubnet-${count.index+1}"
  }
  depends_on = [aws_vpc.myfirstvpc]
}

resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id

  ingress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
  tags = {
    Name = "mySG"
  }
  depends_on = [aws_subnet.myfirstsubnet]
}

resource "aws_instance" "myec2" {
  ami           = "ami-0cb4e786f15603b0d"
  instance_type = "t2.micro"
  key_name = "devops-training"
  vpc_security_group_ids = [ aws_security_group.mySG.id ]
  subnet_id = aws_subnet.myfirstsubnet[0].id
  associate_public_ip_address = true

  tags = {
    Name = "myec2"
  }
  depends_on = [aws_security_group.mySG]

provisioner "remote-exec" {
  inline = [
    "sudo apt-get update -y",
    "sudo apt-get install python -y"
]
}


connection {
   type = "ssh"
   user = "ubuntu"
   private_key = file("./devops-training.pem")
   host = aws_instance.myec2.public_ip
}

}

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