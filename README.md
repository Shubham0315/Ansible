# Ansible

- In job, we tend to do repetitive tasks like server provisioning, configuration management, continuous delivery , app deployment, patchings servers, migrations. To automate the tasks, we simply develop scripts which requires coding skills and regular maintenance
- Here ansible comes into help. We can automate even most complex deployments using ansible playbook which is set of automated instructions. We can even automate tasks on local, DB servers, web servers, cloud we just need to modify a line in playbooks

- Suppose we've no of hosts in our env that we've to restart in specific order, some of them are web based and some are DB. Suppose we've to first down web then db and up db then web ones. We can write ansible playbook to get this done and invoke it to restart our app.
- Also using ansible we can provision resources on public cloud and private cloud like VMs, modify config files, installing app binaries, firewall rules. There are built in modules in ansible which support these operations.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible Configuration Files
-
- When we install ansible, it installs default config files at :- /etc/ansible/ansible.cfg
- This file is divided into below sections where inside each we've no of options and their values, most of them being in default section :-
  - DefaultS :- default locations for inventory files, log files, SSH timeout settings
  - inventory :- to enable certain inventory plugins
  - privilege_escalatio
  - ssh_connection
  - colors
 
![image](https://github.com/user-attachments/assets/4ffd42e9-32e1-4e39-953a-657e0b92b6da)

- By default ansible will take values from cfg file when we run playbooks from anywhere on control node. Suppose we've multiple playbooks for web, db and network, and we need different settings for each of them (like we want facts to be gathered for DB not web, for network we want to extend SSH timeout). In this case we make copy of default config file into each of the 3 directories where 3 cfg files are and make necessary changes in them so that playbooks will pick values from these files. That is one way to override default parameters.

![image](https://github.com/user-attachments/assets/d63d759c-8cdd-44a1-b23f-59308a02dfa5)

- If we want to store one of our cfg files into directory other than our playbooks directory, before running playbook we can pass location to this cfg file to env variable like below so that ansible picks up updated file path instead of default one of our directory
  - Command :- **ANSIBLE_CONFIG=/opt/file.cfg ansible-playbook playbook.yml**
 
- What if we've all of them configured like specifying path in env variable, by creating config file in playbooks dir, or default location. Also we've diff values for diff parameters in each of them. Here in  which order it will consider the cfg files. Here, first priority is to the file where we specify path in env variable(opt/ansible.cfg), inside of playbook dir (/opt/web/ansible.cfg) then default ansible cfg file (etc/ansible/ansible.cfg)

- If we configure playbook for storage env, for that when we dont need a copy of cfg file in our storage dir. When we run ansible, it looks for file inside storage dir, if not it uses one in default location. But we want on eparameter in cfg need to change. So we can override that single parameter using env variable which we can set before executing playbook.
  - Like if we have parameter as       gathering = implicit, we can pas env variable as ANSIBLE_GATHERING=explicit   (if we've to change implicit)
  - Now any value set to env variable like this takes highest precedence
  - We can pass these env varibale in key-value format :-   **ANSIBLE_GATHERING=explicit ansible-playbook playbook.ym**l    (applicable for single playbook execution)
  - To set env varibale in shell :- **export ANSIBLE_GATHERING=explicit** --> **run ansible-playbook playbook.yml**         (applicable for specific shell)
  - If we want to make change persistent across shells/users/systems, create local copy of cfg file in playbook dir and update parameter in it
 
- View Config
  -  List all configurations along with default values :- **ansible-config list** 
  - To see which cfg file is active :- ansible-config view
  - To see which setting is picked by ansible :- ansible-config dump
 
![image](https://github.com/user-attachments/assets/ccef1b74-81d0-4b29-8615-cbd1da56c057)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

