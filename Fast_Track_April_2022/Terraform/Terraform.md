# Terraform

* __Terraform__ is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. 
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


## How to install terraform:
* On windows : 
```sh
choco install terraform
```
* On ubuntu:
```sh
sudo apt-get update 
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get install terraform -y 
terraform --version
```
* To check terraform version

```sh
terraform --version
```

## Authenticate Terraform to speak with AWS: 
* Terraform speak to AWS by using IAM(Identity Access Management).
![preview](../images/tfn1.png)
![preview](../images/tfn2.png)
![preview](../images/tfn3.png)
![preview](../images/tfn4.png)
![preview](../images/tfn5.png)
![preview](../images/tfn6.png)
![preview](../images/tfn7.png)
![preview](../images/tfn8.png)

## Terraform Provider  :

```sh
provider '<name>' {
    <arg1> = <value1>
    <arg2> = <value2>
}
```
* AWS provider terraform template [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPR5AP2COI"
  secret_key = "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"
}
```

## Resource syntax :

```
resource "<resource-type>" "<resource-name>" {
    arg1 = "value1"
      ...
      ..
      argn = "value2"

}
```

## Agruments and Attributes:
* Arguments are the inputs to your resource and attributes are outputs of your resources
![preview](../images/tf9.png)

<br/>
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>


## Amazon VPC & Subnet:
* Amazon __Virtual Private Cloud__ (Amazon VPC) enables you to launch AWS resources into a virtual network that you've defined.
* A __subnet__ is a segmented piece of a larger network. More specifically, subnets are a logical partition of an IP network into multiple, smaller network segments.

### Create VPC & Subnet from AWS console as below :
* __VPC Creation__ :
![Preview](../images/vpc1.png)
![Preview](../images/vpc2.png)
![Preview](../images/vpc3.png)
![Preview](../images/vpc4.png)

* __Subnet creation__ :



###  Terraform template to  create VPC & Subnet in AWS:
* Create in file with extension __.tf__ (vpc-subnet.tf)
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


 
## Create a VPC & Subnet using multi files in the Terraform template:
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
terraform plan -out mutilfile.plan
terraform apply mutilfile.plan
```

![preview](../images/tf10.png)
![preview](../images/tf11.png)


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
* Input variables let you customize aspects of Terraform modules without altering the module's own source code. This allows you to share modules across different Terraform configurations, making your module composable and reusable.
* Terraform variables [REFERHERE](https://www.terraform.io/language/values/variables)

## Use variables to create multiple subnets:
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
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>

## Count in terraform:
* count is a meta-argument defined by the Terraform language. It can be used with modules and with every resource type.
* __count.index__ — The distinct index number (starting with 0) corresponding to this instance.
* __count & count.index__ -- [REFERHERE](https://www.terraform.io/language/meta-arguments/count)

```sh
resource "aws_instance" "server" {
  count = 4 # create four similar four VPC's

  cidr_block       = var.vpccidr
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc-${count.index}"
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



### Use the length in terraform script then  main.tf will change as below:

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
<br/>
<br/>
<br/>

* * * 

<br/>
<br/>
<br/>
<br/>


### Security group:
![preview](../images/tf13.png)

* __Resource: aws_security_group__  --   [REFERHERE(https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)

* After adding SG the main.tf look as below:
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

resource "aws_security_group" "mySG" {
  name        = "mySG"
  description = "mySG"
  vpc_id      = aws_vpc.myfirstvpc.id

  tags = {
    Name = "mySG"
  }
  depends_on = [aws_subnet.myfirstsubnet]
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

### Create s3 bucket using terraform:
* __Resource: aws_s3_bucket__  [REFERHERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket)
```sh
resource "aws_s3_bucket" "myfirstbucket" {
  bucket = "my-first-test-bucket"
  acl    = "private"

  tags = {
    Name        = "myfirstbucket"
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

## DATA sources :
* Data sources are used to query the aws resouces which are already created.

### Create a subnet to  vpc, which is already created in aws.

```sh
provider "aws" {
  region     = "us-east-1"
  access_key = "AKIA3IUVW2N67JAQ2ZIA"
  secret_key = "CiVcsgEOQ5+HFmhqpBbUlatetc7nLl+WJeQ0BhGj"
}


data "aws_vpc" "selected" {
  id = "vpc-0fef1abea454dac56"
}

resource "aws_subnet" "example" {
  vpc_id            = data.aws_vpc.selected.id
  availability_zone = "us-east-1a"
  cidr_block        = cidrsubnet(data.aws_vpc.selected.cidr_block, 4, 1)
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

## Terraform statefile :
* Terraform must store state about your managed infrastructure and configuration. This state is used by Terraform to map real world resources to your configuration, keep track of metadata, and to improve performance for large infrastructures. This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment.


## Terraform Registry 
* Terraform registry is a place where you can find the predefined modules(terrafrom scripts).
![preview](../images/tf14.png)

* For module document [REFER HERE](https://www.terraform.io/docs/configuration/modules.html) and for the syntax of the terraform module [REFER HERE](https://www.terraform.io/docs/modules/index.html)

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
* Copy the singlefile folder to /samplemodule/
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

## EC2 instances creation in terraform 
* AMI , instancetype , no of instances , vpc , subnet , autoassign publicip , tags , SG , keyname.
* the vars.tf and main.tf look like below:
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
  ami           = "ami-0dd9f0e7df0f0a138"
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
* Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction. Provisioners can be used to bootstrap a resource, cleanup before destroy, run configuration management, etc.
* __Terraform Provisionerss__ -- [REFERHERE](https://www.terraform.io/language/resources/provisioners/syntax)
# Terraform provisioning :
* You are assigned with task of creating a vm and installing the necessary softwares init.
* Steps:
  1. Create a VM 
  2. Connection to the VM
  3. Installing necessary softwares

![preview](../images/tf501.png)

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
      "puppet apply",
      "consul join ${aws_instance.web.private_ip}",
    ]
  }
}
```

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
  access_key = "AKIAYZCYFVHPSPURIGOV"
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
  ami           = "ami-0ac73f33a1888c64a"
  instance_type = "t2.medium"
  key_name = "devops-oregon"
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
   private_key = file("./devops-oregon.pem")
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