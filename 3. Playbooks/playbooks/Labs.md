# Problem Statement

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob Password: caleston123 C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob Password: caleston123

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Which of the following formats is the Ansible playbook written in?
- yaml

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Which command would you use to run update_service.yml playbook in check mode?
- ansible-playbook update_service.yml --check

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Which command would you use to run the configure_database.yml playbook in both check mode and diff mode?
- ansible-playbook configure_database.yml --check --diff

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. To check the configure_database.yml playbook for syntax errors, which command would you use?
- ansible-playbook --syntax-check configure_database.yml

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. Which command would you use to run ansible-lint on the database_setup.yml playbook?
- ansible-lint database_setup.yml

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. You've been given feedback from ansible-lint about potential issues in your hypothetical webserver_setup.yml playbook. The feedback mentions issues with indentation, deprecated modules, and missing name attributes. Which of the following is NOT a recommended action based on the feedback?

A. Correcting the indentation in the playbook.
B. Replacing deprecated modules with their newer counterparts.
C. Ignoring the feedback and proceeding with playbook execution.
D. Adding 'name' attributes to tasks that are missing them.

- Ignoring the feedback and proceeding with playbook execution.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

7. If ansible-lint provides no output after checking a playbook, what does it indicate?
- The playbook adheres to best practices and has no style-related issues.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

8. Update the name of the play in /home/bob/playbooks/playbook.yaml playbook to Execute a date command on localhost.
- ![image](https://github.com/user-attachments/assets/f27994da-b95b-4c22-bf2e-e27489ba2a54)
- ![image](https://github.com/user-attachments/assets/b4c82771-c6ea-46cf-b1c6-af934316803d)
- ![image](https://github.com/user-attachments/assets/e5cbfff1-c55e-4a13-a3ad-d68bd048655f)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

9.  Update the playbook /home/bob/playbooks/playbook.yaml to add a task name Task to display hosts file for the existing task.
- ![image](https://github.com/user-attachments/assets/dfeacf13-516d-43a1-b287-7c04e9b9c90d)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

10. We have reset the playbook /home/bob/playbooks/playbook.yaml, now update it to add another task. The new task must execute the command cat /etc/resolv.conf and set its name to Task to display nameservers.
- ![image](https://github.com/user-attachments/assets/e2e7c757-26fa-41aa-8a00-a2d259af95a3)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

11. So far, we have been running all tasks on localhost. We would now like to run these tasks on node01, this host is already defined in /home/bob/playbooks/inventory file. Update the playbook /home/bob/playbooks/playbook.yaml to run the tasks on the node01 host.
- ![image](https://github.com/user-attachments/assets/e1435198-baa6-4ccd-9a18-e751f79acab1)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

12. Refer to the /home/bob/playbooks/inventory file. We would like to run the /home/bob/playbooks/playbook.yaml on all servers defined under web_nodes group.
- ![image](https://github.com/user-attachments/assets/645ce267-8668-4458-8ae1-18fb71c4c697)
- ![image](https://github.com/user-attachments/assets/244a709c-2bba-4714-bb27-529b3fe44d54)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

13. Update the /home/bob/playbooks/playbook.yaml to add a new play named Execute a command on node02, and a task under it to execute cat /etc/hosts command on node02 host, name the task Task to display hosts file on node02.
- ![image](https://github.com/user-attachments/assets/2981be63-5def-4ef7-9048-262c956fb8ca)













