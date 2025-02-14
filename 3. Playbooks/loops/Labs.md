# Problem Statement

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob Password: caleston123 C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob Password: caleston123

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Can loops be executed on dictionary values in Ansible?
- Yes

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Which type of plugin with_* directives use in Ansible?
- lookup

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. The playbook /home/bob/playbooks/fruits.yml currently runs an echo command to print a fruit name. Apply a loop directive (with_items) to the task to print all fruits defined under the fruits variable.
- ![image](https://github.com/user-attachments/assets/1646b986-a211-4db9-a4e7-5430f6ab7a28)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. We are attempting to install multiple packages using the yum module for a more realistic use case. The playbook /home/bob/playbooks/packages.yml installs only a single package. Update it to install all packages defined under packages variable.
- ![image](https://github.com/user-attachments/assets/79939b58-f254-48cb-b203-683a3c5a9ddc)
- ![image](https://github.com/user-attachments/assets/f305d74c-978e-422c-ae8a-71b4d2fff04d)


 
