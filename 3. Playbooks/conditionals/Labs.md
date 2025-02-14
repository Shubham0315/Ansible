# Problem Statement

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123
C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Which of the following Ansible built-in variable populates the flavour of the operating system?
- ansible_os_family

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Which keyword is used to define a condition in an Ansible playbook?
- when

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. There is a playbook named nginx.yaml under /home/bob/playbooks directory. It is starting nginx service on all hosts defined in /home/bob/playbooks/inventory inventory file. Use the when condition to run this task only on node02 host.
- ![image](https://github.com/user-attachments/assets/0c3f73a1-65d6-46b6-a92d-47015e92c0a6)
- ![image](https://github.com/user-attachments/assets/ef36b73e-14d1-4a22-b30f-0d680d4f9f04)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. The playbook under /home/bob/playbooks/age.yaml , has a variable defined called age. The two tasks attempt to print if I am a child or an Adult. Use the when conditional to print if I am a child or an Adult based on whether my age is < 18 (Child) or >= 18 (Adult).
- ![image](https://github.com/user-attachments/assets/6f9b3b9f-567e-4fbc-be97-049d885b0a87)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------











