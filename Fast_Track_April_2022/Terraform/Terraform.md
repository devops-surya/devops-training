# Terraform
* Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share. 

## Understanding of Terraform:
* Terraform is a __infraprovisoning__ tool.
* __Infraprovisoning__ --- What ever you want to create for your project in the cloud is called as infraprovisoning.
* Terraform work on the multiple clouds.
* Terraform supported clouds [REFER HERE](https://registry.terraform.io/browse/providers)
* Any cloud we are using in terraform is called  as __Provider__.
* Whatever you want to create in the terrafrom is called as __Resource__.
* Terraform uses the __configuration language__ to write the terraform script.
![preview](../images/tf1.png)

## Prerequisites:
* Need to create a AWS free tier account.


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

## Create a Ec2 instance and install terraform:
```sh
sudo apt-get update 
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get install terraform -y 
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

## Terraform Provider template :
```sh
provider '<name>' {
    <arg1> = <value1>
    <arg2> = <value2>
}
```

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPR5AP2COI"
  secret_key = "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"
}
```

##  Terraform template to  create VPC in AWS:
* We must know , how to do it manually .
* To create a VPC  basic things required are :
   1. Name of VPC
   2. CIDR block
* Create in file with extension __.tf__ (provider.tf)

```sh
provider "aws" {
  region     = "us-east-2"
  access_key = "AKIAYZCYFVHPR5AP2COI"
  secret_key = "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"
}
resource "aws_vpc" "myfirstvpc1" {
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "default"

  tags = {
    Name = "myfirstvpc1"
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
terraform validate .
```
![preview](../images/tf3.png)

* To run the terraform script 

```sh
terraform apply .
```
![preview](../images/tf4.png)

![preview](../images/tf5.png)

![preview](../images/tf6.png)

![preview](../images/tf7.png)

* To destroy the resource :

```sh
terraform destroy .
```
![preview](../images/tf8.png)


## Agruments and Attributes:
* Arguments are the inputs to your resource and attributes are outputs of your resources
![preview](../images/tf9.png)


## Create a VPC & Subnet using multiple files in the Terraform template:
* Create a folder  multiplefile
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
terraform init .
terraform validate .
terraform apply .
terraform destroy .
terraform plan -out mutilfile.plan
terraform apply mutilfile.plan
```

![preview](../images/tf10.png)
![preview](../images/tf11.png)


## If you came a across a scenario of creating multiple subnets:
1. First case :
    * The main.tf and vars.tf looks like below:
* main.tf
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

* For variables [REFERHERE](https://www.terraform.io/docs/language/values/variables.html)
* vars.tf:
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
* Run the below commands after the above data is replicated:
```sh
terraform init .
terraform validate .
terraform apply .
terraform destroy .
```

2. Second case:
* using count and count.index .
* For count [REFER HERE](https://www.terraform.io/docs/language/meta-arguments/count.html)
* For count.index [REFER HERE](https://www.terraform.io/docs/configuration-0-11/interpolation.html)
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
* For length [REFER HERE](https://www.terraform.io/docs/configuration/functions/length.html)
* After using the length in terraform script the main.tf will change as below:

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

## Depends_on
* For document [REFER HERE](https://www.terraform.io/docs/configuration/resources.html)
* After adding the depends_on to our script , the main.tf looks as below:

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

## Security group:
![preview](../images/tf13.png)

* For document [REFER HERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group)

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
## Create inbound/outbound rules to the securitygroup
* For adding securitygroup rules [REFER HERE](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group_rule)
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

## Create s3 bucket using terraform:
```sh
resource "aws_s3_bucket" "myfirstbucket" {
  bucket = "my-first-test-bucket"
  acl    = "private"

  tags = {
    Name        = "myfirstbucket"
  }
}
```

## DATA sources :
* Data sources are used to query the aws resouces which are already created.
* Create a subnet to  vpc, which is already created in aws.

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
terraform init .
```
![preview](../images/tf15.png)


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

## Provisioners in terrafrom 
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
