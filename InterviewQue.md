How system admins used to perform tasks before ansible?
-
- Before 10 years, devops was not that developed, then there were system admins. Primary task of system admins was configuration management
- Every company used to have own on premises setup and used to have physical servers/virtual machines on private cloud
- Suppose the organization has only 1 sys admin and have 5 physical servers, 4 of which were Linux and 1 was windows
- So sys admin used to install hypervisor and create VM on those physical servers. Primary task of sys admin was to ensure distribution installed on these Linux VMs is up to date (to not have outdated packages, security issues)
- Another task of sys admin was to make sure packages and libraries (wget/curl/openshh) installed on these servers are free from vulnerabilities and application dependencies on these VMs are also secure. Also sys admin must do maintenance of these servers as well (of CPU, Memory and to ensure they are to be available all the time).

- Tasks of sys admins :-
  - Make sure distribution version and system dependencies are up to date
  - Application dependencies such as language, java runtime are up to date
  - install packages on server
  - install up to date dependencies and libraries
  - make sure CPU, memory available all the time
 
- So even to update java version, sys admin had to login to machine and run command. These all things sys admins used to perform manually or using scripts. But shell scripts wont work on windows machines as their distribution is different (can also fail if one have centos Linux and one has Ubuntu Linux)
  In shell script. Where sys admin wrote "yum" command which will work on centOS but will fail on Debian or any other Linux distro. So very hectic thing for admins
- Thus config management was mostly manual (not by scripts)

- Here came config management tools like puppet, chef, ansible

- Puppet/chef used to act as interface between sys admin and organizational configurations. Sys admins used to write puppet/chef programming and they used to automate the things onto servers (using puppet script they can automate servers). So sys admins instead of writing shell script for Linux and powershell script for windows, they can write puppet script to automate tasks on target servers.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How config management tools came to rescue?
-
- Puppet/chef used to act as interface between sys admin and organizational configurations. Sys admins used to write puppet/chef programming and they used to automate the things onto servers (using puppet script they can automate tasks on servers). So sys admins instead of writing shell script for Linux and powershell script for windows, they can write puppet script to automate tasks on target servers.
- Puppet scripts :- to automate tasks on target servers
- Challenge here was we needed to learn complex style of puppet/chef such as ruby. Also puppet was not "agentless in architecture"
  Sys admins needed to go to each VM/physical and need to install agent (software) and needed to connect target machines(machines where to automate) with master (where puppet/chef is installed)

- Challenges with Puppet/chef :-
  - Not agentless, need to install softwares on target servers
  - Need to learn complex style langauges
 
- Ansible advantages :-
  - Agentless architecture, no need to install softwares on target servers
  - Just need top know yml syntax to write playbooks which run on servers
 
- **Control Node (VM Master)** :- Machine on which we install ansible
- **Managed Node (VM Worker)** :- Using master we manage config on these nodes/servers

- Uses of ansible :-
  - Used for config management
  - Powerful automation platform
  - Can do provisioning like create infrastructure, resources on cloud/servers
  - Used for CICD deployment using artifacts. Like using control node, deploy app on multiple K8S clusters
  - Used for network automation
 
- Suppose we've been given a task to install java. We'll write yaml file on control node, run ansible command which can talk to all other VMs (worker), java will be installed and run on all managed nodes (even if distribution of managed nodes is different)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Which is more suitable for automation? Ansible, python or shell scripting?
-
- We can use python/shell/ansible for automating installation of java on VM
- Lets say we are handling 5 VMs. We've to install java on all
  - We can login to each VM and install java manually.
  - We can also write simple shell script "yum install java" and run on VM manually logging on them one by one
  - If one VM is windows, using shell script our automation wont work as we might have different package managers on each VM
  - But python can work for all VM whether it is Linux or windows. So if we write python script and execute on all, it will get the task done. But here we need to know python, timely we have to maintain code, logging to each VM is tedious
  
  - Here ansible works. We dont have to login to VM, just install ansible on control node which reads inventory file (config file) having info of related servers and it will install the required java JDK on each VM. So no manual intervention.

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How to install ansible?
-
- Go to ansible doc and search install ansible. Simplest way to install is using python pip
- We need to have WSL distribution installed on our machine for control node requirements or use EC2 as ansible control node
- Use pip in your selected Python env to install full ansible package for current user
  Command :- **python3 -m pip install --user ansible**
  If we have python installed, just use "pip install ansible"

- After installing, we need some extensions on our VS code (install on VS code)
  YAML (By redhat)
  Ansible (By redhat)

- To check version :- **ansible --version**

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How ansible achieves Authentication?
-
- We install ansible on control (master) node. We provide instructions to ansible on control node with help of yaml(ansible playbooks) or adhoc commands. Instructions can be like install app on managed nodes (servers we want to install through ansible)
- When we try to install app on worker, it will not take our instructions as it will need authentication, be it any VM, Physical server, instance (public, private). Its not possible to talk to physical or VM without authentication

- 2 ways of authentication are :- **SSH keys and Password**

- We can have public key setup on our target (worker) VMs and using private key we can talk to them
- While running ansible, we cant provide password/key everytime for each VM as we're not doing automation. Instead we can setup passwordless authentication between control and managed nodes so ansible will directly execute instructions in yaml.
- So passwordless authentication --> pre-requisite for ansible
- When from our laptop we try to connect to other VM, it will either ask for password or .pem file(ssh key)

- Passwordless authentication is a mechanism where we tell the target VM not to ask for password when we get request from source VM. Initially for the first time only we need to provide password or .pem file
- To communicate with EC2 only way is using SSH key (.pem file)

1. **Using SSH Key**
- Now we have 2 managed node running instances. Go to terminal and run below command
- Command :- ssh-copy-id -f "-o ~/Downloads/file.pem" ubuntu@PublicIP
- For first time only we need to provide .pem file. From second time we can directly do ssh ubuntu@IP to go to VM without even providing .pem file, without aksing for SSH key

![image](https://github.com/user-attachments/assets/90711cd9-cd68-4622-bfbc-91f72a9566c9)
![image](https://github.com/user-attachments/assets/190b7fdf-99b4-4992-b085-ef6321ada271)


2. **Using password**
- Go to EC2 dashboard, connect to the instance and open below file :- **sudo vim /etc/ssh/sshd_config.d/.conf**
- It is a cloud init file used to update ssh config which we need to update as "passwordauthentication" to "yes"
- After that we have to restart the ssh :- **sudo systemctl restart ssh**
- Then run : **sudo passwd ubuntu and update password**
- Now logout and run :-  **ssh-copy-id ubuntu@IP**
- From now on we can connect to EC2 without asking for password

![image](https://github.com/user-attachments/assets/c772580d-3b23-4070-aed7-aa9f1a9948b5)
![image](https://github.com/user-attachments/assets/8784f73f-d809-4f21-8ea4-896c4fa9df82)
![image](https://github.com/user-attachments/assets/3bda8268-7087-4495-83b1-61b4c974ac33)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Explain about ansible inventory
-
- Ansible control node executes instructions on managed nodes. But how control node understand managed nodes are?. There is a way for ansible to know what are its managed nodes
- Inventory is a file in ansible where we put in name of our managed nodes (user, IP). Inventory can be written in 2 formats :- Inventory.ini and yaml
- This file can be at any location on our machine. We just have to pass its path in ansible execution. On many ansible machines, the file is present in form of /etc/ansible/hosts, where "hosts" is inventory file
- Inventory is heart of ansible as it tells control nodes which servers it has to connect with

- There can be requirement we dont want to run command on all servers or on one server
- Lets say there are 10 app servers and 5 DB servers. Here if we put all 15 instances in inventory. We can group servers in inventory file as well

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible adhoc commands
- 
- Ansible adhoc commands are simple one liner commands used to quickly execute tasks on remote hosts without writing a playbook
- They're used for quick troubleshooting, system administration and one time tasks

- Syntax :- ansible <host-pattern> -m <module> -a "<module-arguments>"
  - host-pattern :- Target hosts (from inv or defined in command)
  - -m <module> :- specifies module to use (ping,shell,copy)
  - -a "<module-arguments>" :- arguments for module
 
- Check connectivity :- ansible all -m ping
- Run shell command :- ansible all -m shell "uptime"
- Check disk usage :- ansible all -m command -a "df -h"    #command is module here
- Create file :- ansible all -m file -a "path=/tmp/testfile"
- Copy file :- ansible all -m copy -a "src=/home/user/file.txt dest=/tmp/file.txt"
- Install package :- ansible all -m apt -a "name=nginx state=present" -b
- Restart service :- ansible all -m service -a "name=nginx state=restarted" -b

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Difference between adhoc commands and playbook
-
- Adhoc commands are for one time use whereas playbooks are for reusable automation
- In adhoc we dont need yaml like playbooks
- Adhoc are simple commands and best for quick tasks

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Wht yaml is used ?
-
- We write playbooks in YAML. It is human readable data serialization language
- Suppose for our python application, we need input in form of list of users (data). This can be passed to app using text file, json or yaml
- Text file is not recommended as there is no standard format for that, no syntax for text file
- Here std templating languages like json or yaml comes in. Thats why in devops we use these languages as data is structured in serialized way. Mostly yaml is used as its more human readable unlike JSON

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How to write yaml?
- 
- To learn yaml we need to learn 4 things 
  1. How to write strings, numbers and Booleans in yml. Syntax is :- name:<space>value
     string: Hello World !
     number: 42
     Boolean: true
  2. We need to know when to use list and its syntax
     fruits:
       - apple
       - banana
       - orange
  3. When to use dictionary and its key-value pair
     person:
       name: Hohn
       age: 30
       city: NY
  4. List of dictionaries
 
- While writing yml file, in first line provide 3 hyphens (---)
  #string
  name: Shubham     #string
  age: 26

  #List 
  Tasks:
    - Monitoring
    - CICD Automation

  #Dictionary
  Address:
    street: NY
    city: anagar

- For each item in list use - whereas for each item in dictionary dont use hyphen as they are key value pairs

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Explain ansible playbook structure
-
- Playbook is a list of plays
- Lets say our task is to setup DB server as well as app server. So both's installation and configurations can be written is different plays.

![image](https://github.com/user-attachments/assets/1dfeeaf3-9767-43e8-9fa9-a7159120529e)

- Ansible playbook follows structured format, typically written in yaml

![image](https://github.com/user-attachments/assets/95278e33-90ec-4f89-9723-9b4562537ba2)

  - name :- name of playbook
  - hosts :- target machines on which we want to execute plays on
  - vars :- defines variables that can be used throughout playbook
  - tasks :- list of tasks inside each play
  - handlers :- Used to define tasks triggered by other tasks (restart after config file change)
  - roles :- Specifies reusable role named that contain predefined tasks, handlers, templates, variables

- Playbook is list of plays and within each play we have things like hosts, remote_user, tasks (list), modules in each tasks. Modules perform execution of actions using ansible
- To install apache and deploy. Here in tasks, first task is install apache3 server and 2nd task is to copy the index.html file and put in /var/www/html folder


![image](https://github.com/user-attachments/assets/c8d3b4dd-afed-4bf0-a35f-46550f7d43cd)
