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

  
