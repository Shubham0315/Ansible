- Ansible Modules are categirozed into various groups based on their functionality

1. System modules :- Actions to be performed at system level. Modifying users, groups, host, restart
2. Command Modules :- Used to execute command or script on host. Includes command, expect, shell, script modules
3. File modules :- Help work with files. Acl module to set and retrieve acl info, archive for compression, find/replace to modify contents of existing files
4. Database modules :- Help working with databases like mongodb, mysql, mssql, postgresql
5. Cloud modules :- Modules for various cloud providers like amazon, azure, google, docker
6. Windows modules :- Helps us use ansible in windows env. win_copy, win_command, win_file, win_msi.

---- There are lot of more modules 


1. Command Module
- Used to execute command on remote node. There're various parameter in command module

![image](https://github.com/user-attachments/assets/d31a5448-913e-4f16-8e1c-f23a8559e3a2)

- Here to execute command after changing directory

![image](https://github.com/user-attachments/assets/00783ffd-c512-4c8b-b5ba-22e9a7654a28)

- Creates parameter is used to perform a check before command is run. To create folder command will run only if folder doesnt exist
- free_form parameter means the module takes free_form command to run. Like in below ss, mkdir is free form. Similarly copy requires source and destination as parameters

![image](https://github.com/user-attachments/assets/00c4cdb0-0d60-4b84-beb5-a445af73014d)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Script Module
- Executes script loacted locally on ansible control node on remote nodes after transferring it. To run script of 100s of servers, we dont have to copy it on all servers, ansible does it and runs it on them
- This is done through very simple paly like below. Use script module and specify location of script on ansible control node along with arguments

![image](https://github.com/user-attachments/assets/44777955-f353-4bef-8517-f02c3cf09093)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Service Module
- Used to maintain services on system. Start, stop, restart.
- Below playbook is used to start services in specific order. Here it is not free_form so need to specify in key value pair
- We use name parameter to specify name of service we wish to start and its state.

![image](https://github.com/user-attachments/assets/3bec76ad-cc7b-4fbe-b814-2a2c17b3c922)

- We can also write this playbook in dictionary and map format like below. Name and state are properties of service

![image](https://github.com/user-attachments/assets/e7350754-b2db-4616-a9e9-416fb1f41b02)

- Lets add more tasks to start httpd service followed by nginx service

![image](https://github.com/user-attachments/assets/af93accf-b9a7-4778-9a86-bd0b1372e345)

- Here we use "started" not "start". If we've to instruct ansible to start service we'' "start". Here we're not instructing ansible to start service instead we're instructing to ensure that the service is started
- This means if service is not started, start it. If is already started, dont do anything

- So if we run the playbook again, it wont do anything.

4. lineinfile module
- Used to search for a line in file and replace it or add it if it doesnt exist.
- Suppose we've to add new server in conf file. Below playbook using "lineinfile" task adds new name server info to conf file.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
