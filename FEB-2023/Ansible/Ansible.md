## BASIC PIPELINE OF DEVOPS :
![preview](../images/jenkins1.png)

## Ansible
* Ansible is one of the configuration management tool.
* Ansible is an open-source automation tool used for IT tasks such as application deployment, configuration management, and infrastructure orchestration. It uses a simple and easy-to-learn YAML-based language to define tasks and playbooks, making it accessible to a wide range of users.

<br/>

* * * 

<br/>

## Configuration management :
* For any application to be work,  we need some softwares to be installed. The process of configure & installing softwares is called Configuration Management.

<br/>

* * * 

<br/>

## Ways to install Softwares : 
### Manual :
* Administrator will install  all the softwares.

### Configuration Management:
* We write the desired state ..i,e(i want a file to be created)
* It uses declarative syntax.
* The main usecase of CM tool are idempotency .

<br/>

* * * 

<br/>

## Push / Pull type CM :

### Push type CM : 
* Ansible is the push type model of CM.

![preview](../img/PA1.png)

### Pull type CM:
* Chef is the  pull type model of CM 
![preview](../img/PC1.png)

<br/>

* * * 

<br/>

## Architecture  of ansible :
![preview](../img/AA1.png)

### Playbook:
* In playbook we will define the desired state .
* Playbooks are written in YAML format and consist of a set of tasks that define what actions Ansible should take on the managed hosts.

### Inventory : 
* In Ansible, an inventory file is a simple text file that contains a list of hosts or IP addresses that Ansible can connect to and manage. It is essentially a collection of the hosts or nodes that you want to configure or manage with Ansible.


<br/>

* * * 

<br/>



## SCENARIO-1 :-  LAB SETUP of ANSIBLE  :

![preview](../images/nansible5.png)

* For ansible to be worked we need to install python on all the servers where you  want to install softwares.
* We also have to make sure that python is installed on the ACS , however it will be installed while installing ansible.

1. Enabling the password based authentication both  on ACS and NODE-1 :
```
sudo su - 
vi /etc/ssh/sshd_config
sudo service ssh restart 
sudo service ssh status
ctrl+c or Q -- to exit 
```
![preview](../images/nansible1.png)
![preview](../images/ansible6.png)

2. Create a user and give sudo acess on both ACS and NODE1 servers : 

```
sudo su - 
adduser devops
visudo  
*  To exit : ctrl+X , Y/N , Enter
su devops   
```
![preview](../images/ansible7.png)
![preview](../images/ansible8.png)

3. ssh-keygen on ACS Server to create keys for Key-based Authentication

```
sudo su - devops
ssh-keygen  
ssh-copy-id devops@<nodeipadress>
``` 
![preview](../images/ansible9.png)
![preview](../images/ansible10.png)

4. Ansible installation  on ACS SERVER: 
* Ansible installation [REFER HERE](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu)

```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

5. Installing  python on the NODE1: 

```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install python
```
<br/>

* * * 

<br/>



## Inventory :
* An inventory file is a simple text file that contains information about your hosts or devices, such as their IP addresses, hostnames, and connection details.
* The default path of inventory is 

```
/etc/ansible/hosts
```

<br/>

* * * 

<br/>


## Check the communication b/w ACS and NODE-1:

* Add your NODE-1 public ip to the /etc/ansible/hosts file

```
ansible -m ping all
```

![preview](../images/ansible11.png)

<br/>

* * * 

<br/>



## Use customized file for inventory: 
* Add your NODE1 public ip to the /home/devops/hosts file

![preview](../img/ANS1.png)

* Use below command to check communication between ACS & NODE1

```
ansible -i <path to the file> -m ping all
```
* EX : ansible -i /home/devops/hosts -m ping all

![preview](../img/CIA.png)



<br/>

* * * 

<br/>


## How to write ansible playbooks :
* list down all the manaul commands for the desired state.
* Make sure that the commands are working , when doing manaully .
* Each desired state / each step you are going to do in ansible is considered as task.
* In Ansible the tasks are executed by using MODULES.
* Modules are atomic units of ansible which performs execution

## Playbook syntax:
* Yaml Syntax [REFERHERE(]https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)
* Ansible modules Offical Document [REFER HERE](https://docs.ansible.com/ansible/2.8/modules/list_of_all_modules.html)

![preview](../img/PS1.png)


```
---
- hosts: all
  become: yes
  tasks:
    - name: name of your task1
      module:
        par1: val1
        par2: val2
    - name: name of your task2
      module:
        par1: val1
        par2: val2
  ...
  ..
  ..

```

<br/>

* * * 

<br/>

## SCENARIO-2: Write a playbook to install Tomcat & Java to configure servers:

```
Java is a developement softwares and it is prequisite for Tomcat.
Tomcat is one of the appliaction server.
```
![preview](../img/ANS1.png)


## List down the steps to install tomcat:

```
sudo apt-get update 
sudo apt-get install openjdk-11-jdk
java -version

sudo apt-get update
sudo apt-get install tomcat9

sudo service tomcat9 restart
sudo service tomcat9 status
```
![preview](../images/nansible14.png)



## Playbook to install java11 and tomcat9

```
---
- hosts: all
  become: yes
  tasks:
    - name: installing java 11
      apt:
        name: openjdk-11-jdk
        state: present
        update_cache: yes
    - name: installing tomcat9
      apt: 
        name: tomcat9
        state: present
        update_cache: yes
    - name: restart the tomcat9
      service:
         name: tomcat9
         state: restarted
    
```
* ***NOTE***: Make sure you addd your NODE1 public ip to the /home/devops/hosts file
![preview](../img/ANS1.png)


* To check the playbook syntax is correct : 

```
 ansible-playbook -i /home/devops/hosts playbook.yml --syntax-check
```
![preview](../img/ANS3.png)


* To run the playbook use below command : 

```
 ansible-playbook -i /home/devops/hosts playbook.yml
```
![preview](../img/ANS2.png)



* To run the playbook for the  dryrun 

```
 ansible-playbook -i inventory playbook.yml --check
```

![preview](../img/ANS4.png)


<br/>

* * * 

<br/>

## Playbook vc Adhoc commands :
* Playbooks and Ad-hoc commands are different ways of using Ansible to achieve the same result: configure and manage systems.
* We can define all the tasks and modules in a file (playbook file).
* In adhoc commands , we can use  only one module at at time.

*  Adhoc commands syntax:

```
ansible -i <host file path> -m <module> "para1=value1 ....paran=valuen" [-b]  <all>
```

* For the adhoc commands [REFER HERE](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html)

<br/>

* * * 

<br/>




## SCENARIO -3 : Run the playbook on the specific server in the inventory file.

![preview](../img/AS3.png)

* The  /home/devops/hosts file changes as below :
![preview](../img/ANS5.png)

* Create a java.yml with below playbook  content : 

```
sudo su - devops 
cd /home/devops
vi java.yml 

Paste the below Playbook content 

```

```
---
- hosts: Node1
  become: yes
  tasks:
    - name: installing java 11
      apt:
        name: openjdk-11-jdk
        state: present
        update_cache: yes
```


* To run the playbook use below command : 

```
 ansible-playbook -i /home/devops/hosts java.yml
```
![preview](../img/ANS6.png)



<br/>

* * * 

<br/>


## Reuse ansible playbooks by using  variables :
* In ansible we had a below ways to define variable:
1. host level
2. group level 
3. playbook level 
4. commandline level

* Create variable name **package_name** as below in playbook :
```
---
- hosts: webserver
  become: yes
  tasks:
    - name: using variables in ansible
      apt:
        name: "{{package_name}}"
        state: present
        update_cache: yes

```

1. **Host level variable**  :

![preview](../img/ANS8.png)

2. **Group level variable** : 

![preview](../img/ANS9.png)


3. **Playbook level variable** :

```
- hosts: webserver
  become: yes
  vars:
    package_name:
      - tomcat9
  tasks:
    - name: using variables in ansible
      apt:
        name: "{{package_name}}"
        state: present
        update_cache: yes

```

4 **commandline level variable** :

```
 ansible-playbook -i <hostspath> -e " package_name=tomcat9" playbook.yml
```

<br/>

* * * 

<br/>

## SCENARIO-4 :  sample deployment of apache and php modules:
* Reference Sample Link : [Apache_PHP_Installation](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04)

* **Apache** is a popular open-source web server software that is used to serve websites and web applications over the internet. It was developed by the Apache Software Foundation and is available for a variety of operating systems, including Windows, macOS, and Linux.

* Apache is highly customizable and supports a variety of programming languages, including PHP, Python, Perl, and Ruby. It also supports many different modules and plugins, allowing users to add functionality to their web servers as needed.

* Apache is known for its reliability, scalability, and security, and is widely used by businesses and individuals around the world. It is a key component of the LAMP (Linux, Apache, MySQL, PHP) and LEMP (Linux, Nginx, MySQL, PHP) stacks, which are commonly used for web development and hosting.

* **PHP (Hypertext Preprocessor)** is a popular server-side scripting language that is widely used for web development. It was originally created in 1994 by Rasmus Lerdorf, and has since evolved into a powerful language that is used by millions of developers worldwide.

* list down the manual steps :

```
sudo apt-get update 
sudo apt-get  install apache2 -y 
sudo systemctl enable apache2
sudo apt-get install php libapache2-mod-php php-mysql php-cli -y 
sudo vi /var/www/html/info.php
<?php
phpinfo();
?>
sudo systemctl restart apache2
```

* The playbook looks as below once after convert the manual steps in to tasks :

```
---
- hosts: all
  become: yes
  tasks:
    - name: installing apache2
      apt:
        name: apache2
        state: present
        update_cache: yes
    - name: enable apache2
      service:
        name: apache2
        enabled: yes
        state: restarted
    - name: installing php modules
      apt:
        name: "{{ item }}"
        state: present  
        update_cache: yes
      loop:
        - php
        - libapache2-mod-php
        - php-mysql
        - php-cli

    - name: creating the file info.php
      file:
        path: /var/www/html/info.php
        state: touch

    - name: add content to the info.php file
      blockinfile:
        path: /var/www/html/info.php
        block: |
          <?php
          phpinfo();
          ?>
    - name: restart the apache
      service:
         name: apache2
         state: restarted

```

* Create a file with apache2php.yml  with above content .

```
sudo su - devops 

vi apache2php.yml 

Insert mode 
copy the above playbook content 

ESC:wq                  -- To save the file 

```


*  To check the syntactical errors in playbook:

```
ansible-playbook -i hosts apache2php.yml --syntax-check
```

*  Trial run  :

```
ansible-playbook -i hosts apache2php.yml --check
```
![preview](../images/ansible19.png)
![preview](../images/ansible20.png)


*  To see the apache & php modules installed on browser  :

```
<publicipaddress>  --in the browser
```
![preview](../images/ansible17.png)
![preview](../images/ansible18.png)



<br/>

* * * 

<br/>


## SCENARIO-5 :  sample deployment of apache and php modules on redhat/centos 

* Below are the maual steps : 

```
sudo yum update 
sudo yum  install httpd -y 
sudo systemctl enable httpd
sudo yum install php libapache2-mod-php php-mysql php-cli -y 
sudo vi /var/www/html/info.php
<?php
phpinfo();
?>
sudo systemctl restart httpd

```

* **Exercise** : Write a playbook for above manual steps 




<br/>

* * * 

<br/>


## Mostly used modules in the ansible for install & configure softwares:

* apt 
* yum 
* package
* service
* file
* copy
* blockinfile
* lineinfile

<br/>

* * * 

<br/>



## Ansible conditionals:
* Full document here [REFER HERE](https://docs.ansible.com/ansible/latest/user_guide/playbooks_conditionals.html)

```
---
- hosts: ubuntu
  become: yes
  tasks:
    - name: installing apache2
      apt:
        name: apache2
        state: present
        update_cache: yes
      when: ansible_facts['os_family'] == "Debian"
```

<br/>

* * * 

<br/>


## Fail module:

```
---
- hosts: ubuntu
  become: yes
  tasks:
    - name: fail if the os is other than the debian
      fail:
        msg: the playbook run only for the debian os
      when: ansible_facts['os_family'] != "Debian"
    - name: installing apache2
      apt:
        name: apache2
        state: present
        update_cache: yes
      when: ansible_facts['os_family'] == "Debian"
```


<br/>

* * * 

<br/>

## Package module :
* This module is used to install the both centos and ubuntu packages

```
---
- hosts: ubuntu
  become: yes
  tasks:
    - name: installing apache2
      package:
        name: apache2/httpd
        state: present
        update_cache: yes
```

<br/>

* * * 

<br/>


## If you  didnt find any module /  unable to get the exact modules.

* We have modules in ansible , where we can provide the linux command as it is and run the playbook.
* Examples : shell and command modules

1. SHELL 

SYNTAX:

```
- name: shell module
  shell: sudo apt-get update 
```
2. COMMAND :

SYNTAX:

```
- name: Command module 
  command: sudo apt-get update
```
* ***NOTE*** : In Shell and command modules there wont be any idempotency.

<br/>

* * * 

<br/>

## Basic pipeline with ansible:

![preview](../images/ansible21.png)

```
---
- hosts: all
  become: yes 
  tasks: 
    - name: installing java 
      apt:
        name: openjdk-11-jdk
        state: present
        update_cache: yes
    - name: installing tomcat9
      apt:
        name: tomcat9
        state: present 
        update_cache: yes
    - name: copying the war file
      copy:
        src: /home/devops/SampleWebApp.war
        dest: /var/lib/tomcat9/webapps/
    - name: restart the tomcat9
      service:
        name: tomcat9
        state: restarted

```
* For war [REFER HERE](https://github.com/AKSarav/SampleWebApp/raw/master/dist/SampleWebApp.war)


```
ansible-playbook -i hosts tomcat1.yml --syntac-check

ansible-playbook -i hosts tomcat1.yml
```

![preview](../images/ansible22.png)


### ANSIBLE:
1. Mostly used modules are copy, apt , yum , package , service , systemd , file , blockinfile , lineinfile .
2. Tomcat home path is /var/lib/tomcat9/webapps/ . It runs on the port 8080 . Tomcat logs will be on the folder /var/log/tomcat9/ .


## Exercise:
* Run the playbbok with below tasks :
   * Install java 
   * Install tomcat9
   * Stop the tomcat9
   * Copy the sample war to the /var/lib/tomcat9/webapps/
   * Restart the tomcat9
* When you are running the above playbook for the second time change the playbook as per below tasks:
   * Stop the tomcat9
   * Take the backup of the exising code which is in /var/lib/tomcat9/webapps/
   * Copy the sample war to the /var/lib/tomcat9/webapps/
   * Restart the tomcat9

## Handler in ansible
* Handler is  also one of the module in ansible . It is mostly used to optimise the playbook.
* For Example 

```
---
- hosts: all
  become: yes
  tasks:
    - name: installing apache2
      apt:
        name: apache2
        state: present
        update_cache: yes
      notify:
      - restart apache2
    - name: installing php modules
      apt:
        name: "{{ item }}"
        state: present  
        update_cache: yes
      loop:
        - php
        - libapache2-mod-php
        - php-mysql
        - php-cli

    - name: creating the file info.php
      file:
        path: /var/www/html/info.php
        state: touch

    - name: add content to the info.php file
      blockinfile:
        path: /var/www/html/info.php
        block: |
          <?php
          phpinfo();
          ?>
      notify:
      - restart apache2 
    handlers:
      - name: restart apache2 
        service:
          name: apache2
          enabled: yes 
          state: restarted
```


```
---
- hosts: all
  become: yes
  tasks:
  - name: install apcahe2
    apt:
      name: apache2
      state: present
      update_cache: yes
    notify:
    - restartapache2
  handlers:
    - name : restartapache2
      service:
        name: apache2
        state: restarted

```


## Ansible facts
* For the documents [REFER HERE](https://docs.ansible.com/ansible/latest/user_guide/playbooks_vars_facts.html#id3)

## Reusability of ansible playbooks.
1. VARIABLES
2. IMPORT/INCLUDE
3. ANSIBLE ROLES



## 1. VARIABLES

```
---
- hosts: all
  become: yes
  tasks:
    - name: installing software 
      apt:
        name: {{ package_name }}
        state: present
        update_cache: yes
```

```
ansible-plybook -i hosts -e package_name=git  playbook.yml
```
## 2. Import/Include
* java playbook (java.yml) 

```
- hosts: all
  become: yes 
  tasks: 
    - name: installing java 
      apt:
        name: openjdk-8-jdk
        state: present
        update_cache: yes
```


* Using the java playbook in installing tomcat9

```
- import_playbook: java.yml
- hosts: all
  become: yes 
  tasks: 
    - name: installing tomcat9
      apt:
        name: tomcat9
        state: present 
        update_cache: yes
    - name: copying the war file
      copy:
        src: /home/devops/SampleWebApp.war
        dest: /var/lib/tomcat9/webapps/
    - name: restart the tomcat9
      service:
        name: tomcat9
        state: restarted
```

## 3. ANSIBLE ROLES:
* Ansible roles are the best way of reusing the playbooks :
 We need to understand about the ansible-galaxy [REFER HERE](https://galaxy.ansible.com/)

## Jinja template
* These are used to create the dynamic files. Dynamic files means the content in the file will not be the static
* Example:
* Create a file with extension .j2 
```
vi   Testjinja.txt.j2

This is for the os {{ ansible_os_family }}
This is of distribution {{ ansible_distribution }}
```

* playbook  using jinja template

```
---
- hosts: all
  become: yes
  tasks:
    - name: copying jinja file to the node
      template:
        src: /home/devops/Readme.txt.j2
        dest: /home/devops/
        
```

* Run above playbook by using below command:

```
ansible-playbook -i hosts jinja.yml
```

* After running the above playbook the content in the file changes as below:

```
This is for the os "Debian"
This is of distribution "Ubuntu"

```

## Ansible roles 
* Ansible galaxy link [REFER HERE](https://galaxy.ansible.com/)

## How to use the role from ansible galaxy:
```
 ansible-galaxy install geerlingguy.java
```

![preview](../images/ansible23.png)

## How to use the ansible role downloaded from the ansible-galaxy:

```
---
- hosts: all
  become: yes 
  roles: 
    - role: geerlingguy.java
```

## How to create a ansible role:

```
ansible-galaxy role init <name of role>
```
![preview](../images/ansible24.png)

## Writing Ansible-role to install JAVA 

* Creating a role 
```
ansible-galaxy role init javarole
tree javarole
```
![preview](../images/n1.png)
![preview](../images/n2.png)

* Do  tasks/main.yml as below :
```
---
- name: installing java
  apt:
    name: openjdk-8-jdk
    state: present
    update_cache: yes

```
![preview](../images/n3.png)

* Now use the javarole in your playbook :
![preview](../images/n4.png)

```
---
- hosts: all
  become: yes
  roles:
    - javarole


```
* Run the above playbook using below command:

```
ansible-playbook -i hosts usingjavarole.yml
```

![preview](../images/n5.png)


## Tags in Ansible:
* If you have a large playbook, it may become useful to be able to run only a specific part of it rather than running everything in the playbook. Ansible supports a “tags:” attribute for this reason.

* Tags --  [ReferHere](https://docs.ansible.com/ansible/2.9/user_guide/playbooks_tags.html) 

* Playbook with tags :

```
---
- hosts: all
  become: yes
  tasks:
    - name : Install Tree
      apt:
        name: tree
        state: present
      tags:
      - tree
    - name: install java
      apt: 
        name: openjdk-11-jdk
        state: present
      tags:
      - java
```
1. Run the taks in the playbook which has tag of ```tree```
 

```
ansible-playbook -i hosts tags.yml --tags "tree"
```
![preview](../images/n6.png)

2. Now skip the tasks which has tag of ```tree```

```
ansible-playbook -i hosts tags.yml --skip-tags "tree"

```
![preview](../images/n7.png)


## How to deal with ansible:
1. List down the commands/steps to installed the software
2. My goal is to install tree
```
sudo apt-get update 
sudo apt-get install tree
```

```
yum update
yum install tree
```

### Write a playbook for installing tree : 

```
---
- hosts: all
  become: yes
  tasks:
    - name: installing tree
      apt:
        name: tree
        state: present
        update_cache: yes
```

## Ansible::
* Ansible is a configuration management tool , we can do deployment as well as configuration management by using ansible .
* Ansible is a push type model of CM 
* Ansible uses yaml syntax to write the playbook . But internally ansible is written in python
* YAML - Yet Another Markup Language
* Playbooks -- We write playbooks in ansible to mention our desiredstate/tasks to be done.
* Inventory/hosts -- Where we will provide the nodes information (ipaddress/hostname)
* Writing host file in different sections 
* Modules -- parameters.
* Examples of modules : apt , yum , service , systemd , file , copy  , package , Lineinfile, blockinfile , tags , fail
* Looping in ansible 
* Conditionals in ansible 
* Different types of defining variables -- host, group , playbook,commandline
* Resuability of playbooks : 1. variables 2.import/include 3. Ansible roles 
* APache and php installation -- LAMP installation
* Installing java , tomcat 
* Created a devops pipeline by using the samplewarfilefrom opensource.
* Deployed the application by using ansible


1. List down manual commands.
2. Check it by running them manually 
3. try to automate it by using the playbook (exact module)
4. create a inventory/host file -- Run the playbook 