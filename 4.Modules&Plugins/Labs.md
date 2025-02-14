# Problem Statement

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123
C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Which of the following Ansible modules support free_form parameter?
- command

2. Does Ansible support idempotancy?
- Yes

3. Which of the following commands we can use to see the information about Ansible modules from command line?
- ansible-doc

4. Which of the following statements are true about lineinfile Ansible module?
-  It only adds the given line in file if that line doesn't exist in that file.
- It keeps the existing lines as well and add a new given line in the file.

5. What are Ansible system modules used for?
- System modules are actions to be performed at a system level such as modifying the users and groups on a system, modifying iptables, starting/stopping the service etc.

6. Your organization uses a proprietary cloud service that is not natively supported by Ansible. You need to develop a custom Ansible module to interact with this cloud service's API and provision resources. Which type of the Ansible plugins allows you to integrate with a cloud provider's API for custom resource provisioning?
- Module plugin

7. You are tasked with setting up an Ansible playbook that automates the deployment of applications on AWS ec2 instances. Before running the playbook, you need to ensure that Ansible has an up-to-date inventory of all ec2 instances in your AWS account. Which type of Ansible plugin would you use to fetch real-time information about your AWS ec2 instances?
- Dynamic Inventory Plugin

8. You have a custom dynamic inventory script named aws_inventory.py. Which command would you use to list all hosts in your AWS inventory using this script?
- ansible-inventory --list -i aws_inventory.py

9. You are tasked with finding a collection in Ansible that provides modules specifically designed for managing Cisco IOS devices. Using the Modules & Plugins Index, which of the following collections is best suited for this purpose?
- cisco.ios

10. Which of the following is not a common connection parameter used by modules within the cisco.ios collection for managing Cisco IOS devices?
- ios_version

11. Which of the following Ansible versions is cisco.ios module likely to be compatible with? Note: This can be a hypothetical answer; the actual version compatibility would need to be checked in the Modules & Plugins Index.
- ansible 2.8

12. You're planning to deploy an application on AWS and need to set up ec2 instances using Ansible. Which module is primarily used for managing ec2 instances?
- ec2_instance

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

13. Update the playbook named playbook.yaml under /home/bob/playbooks directory with a task named Execute a script to run a script. The script is located at /tmp/install_script.sh on student-node. Use the script module.
- ![image](https://github.com/user-attachments/assets/894e0b6e-3429-4140-8309-a1281ec1a68c)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

14. Update the playbook /home/bob/playbooks/playbook.yaml to add a new task to start httpd service on all web nodes defined in /home/bob/playbooks/inventory file. Use the service module. 
- <img width="509" alt="image" src="https://github.com/user-attachments/assets/4fa3c77f-9c3c-4996-8190-eda8f9490a32" />

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

15. Update the playbook /home/bob/playbooks/playbook.yaml to append the /var/www/html/index.html file on all web nodes. The line needs to be added is Welcome to ansible-beginning course, create the index.html file if doesn't exist. Use the lineinfile module.
- ![image](https://github.com/user-attachments/assets/0d76772e-9205-4870-88d5-a9857651a87b)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------




