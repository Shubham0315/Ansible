# Problem Statement
-

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123
C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Can we define variables in an Ansible inventory file?
- Yes

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Can we define variables in an Ansible playbook?
- Yes

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Which of the following formats is used to call a variable in an Ansible playbook?
- '{{ variable_name }}'

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. The /home/bob/playbooks/playbook.yaml playbook is adding a name server entry in /tmp/resolv.conf sample file on localhost. The name server information is already added to the /home/bob/playbooks/inventory file as a variable called nameserver_ip.
Replace the hardcoded ip address of the name server in this playbook to use the value from the variable defined in the inventory file.

- ![image](https://github.com/user-attachments/assets/c098fc0f-70c5-4efa-bf9e-f370b7a734e3)
- ![image](https://github.com/user-attachments/assets/7f02d7ea-8fa9-437d-8a2a-33e191f88551)

- Solution :- ![image](https://github.com/user-attachments/assets/578eb5fc-6c2d-474b-abee-6373d87e80da)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. We have updated the /home/bob/playbooks/playbook.yaml playbook to add a new task to disable SNMP port on localhost. However, the port is hardcoded in the playbook. Update the playbook to replace the hardcoded value of the SNMP port to use the value from the variable named snmp_port, defined in the inventory file.

- ![image](https://github.com/user-attachments/assets/fc717064-5262-40a2-939d-f9b502848d36)
- ![image](https://github.com/user-attachments/assets/31803cb7-83ab-404b-9317-a9a6c455b775)

- Solution :- ![image](https://github.com/user-attachments/assets/c5782c1b-8180-427b-bc98-95f38c1c486f)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. We have reset the /home/bob/playbooks/playbook.yaml playbook. Its printing some personal information of an employee. We would like to move the car_model, country_name and title values to the respective variables, and these variables should be defined at the play level.
Add three new variables named car_model, country_name and title under the play and move the values over there. Use these variables within the task to remove the hardcoded values.

- ![image](https://github.com/user-attachments/assets/78978bbc-6a8c-4a90-b47f-8eaab49fa7de)

- Solution :- ![image](https://github.com/user-attachments/assets/17f831b1-81ff-41cb-b40d-4f4ead3cbd04)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

7. The /home/bob/playbooks/app_install.yaml playbook is responsible for installing a list of packages on a remote server(s). The list of packages to be installed is already added to the /home/bob/playbooks/inventory file as a list variable called app_list.
Right now the list of packages to be installed is hardcoded in the playbook. Update the /home/bob/playbooks/app_install.yaml playbook to replace the hardcoded list of packages to use the values from the app_list variable defined in the inventory file. Once updated, please run the playbook once to make sure it works fine.

- ![image](https://github.com/user-attachments/assets/3856be1a-95bd-4e9c-af09-86af8ea7580f)
- ![image](https://github.com/user-attachments/assets/dc0b53b2-ea52-4631-a7ab-bb533946ec6e)

- Solution :- ![image](https://github.com/user-attachments/assets/8c0c4b14-ac24-49f2-b2b3-f337ab49ccc6)
- ![image](https://github.com/user-attachments/assets/0b5df03e-4890-4db8-b71a-526fef6fd18e)
- ![image](https://github.com/user-attachments/assets/03a9d7a6-1677-43a9-a31b-5d6c3a15e57f)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

8. The /home/bob/playbooks/user_setup.yaml playbook is responsible for setting up a new user on a remote server(s). The user details like username, password, and email are already added to the /home/bob/playbooks/inventory file as a dictionary variable called user_details.
Right now the user details is hardcoded in the playbook. Update the /home/bob/playbooks/user_setup.yaml playbook to replace the hardcoded values to use the values from the user_details variable defined in the inventory file. Once updated, please run the playbook once to make sure it works fine.

- ![image](https://github.com/user-attachments/assets/c76cad55-f38f-4ecf-9cea-3f86d68aceb0)
- ![image](https://github.com/user-attachments/assets/38306dc8-160f-43c6-a3f8-9dede45166bf)

- Solution :- ![image](https://github.com/user-attachments/assets/5abc2327-0814-4b46-9793-00bb497c80eb)
- ![image](https://github.com/user-attachments/assets/c8f7aeba-ee27-43fc-81d9-d444e4d15401)
