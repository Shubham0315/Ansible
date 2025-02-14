Ansible Playbooks
-

- Ansible playbooks are orchestration language for ansible as we define what tasks to perform in form of set of instructions.
- These instructions can be running commands on servers and restarting those servers in specific order
- It can be as complex as deploying 100s of VMs on public and private cloud, provision storage to VMs, setting up their network config, configuring apps on them, setting up LB, setting up monitoring , etc

- All playbooks are written in yaml format. Play means set of tasks to be run on single or group of hosts. Task is an action performed on host like executing command, running shell script, install package, restart,etc.

- Below is example of platbook to perform activities on localhost

![image](https://github.com/user-attachments/assets/05648f13-6952-47f8-9e36-73c9e082422d)

- Sample playbook format. Lets split list of tasks in 2 separate plays in our above playbook. So we can say playbook is a list of dictionatries in yaml terms.
  - Each play here is a dictionary having set of properties called name, host and tasks (order of prop in dictionary doesnt matter as it is unordered). But in tasks the order matter as it is list or array and is ordered collection.
  - So if we define to start service before installing, it will not happen. 

![image](https://github.com/user-attachments/assets/64d46c36-5de7-425e-9f01-8388a539678e)

- Hosts parameter indicates which host we want those operations to run on. Host on which we want to perform operations is always set at play level. Host defined in inv file must match host in playbook so that host connection info is retrieved from inv file.
  - If we specify group, tasks will be performed on all hosts listed under the group simultaneously.

![image](https://github.com/user-attachments/assets/a97c2504-ec9f-4cf1-b542-45c48d85996b)

- Modules are different actions run by tasks. In our above yaml command, script, service are modules
- Once we successfully build the ansible playbook, we can run them by using below commands :- **ansible-playbook playbook.yml**

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Verifying Playbooks
-
- Suppose we've to deploy critical software update to 100s of servers in our organization, we'll write ansible playbook to automate the task and we run on prod.
- But dues to error in playbook, instead of updating software, it shuts down service on all servers resulting in downtime and challenge to restore the service. Due to this we must verify the playbook in playbook development process

- Why to verify playbooks?
  - It allows us to catch and rectify any errors or unexpected behavior in a controlled env which can lead to downtime or data loss. Verification saves you from potential headaches.
 
- Ansible provides several modes to verify playbooks :- check mode , diff mode
- **Check mode** :- dry run mode where ansible executes playbook without making any actual changes on host. Allows to view playbook changes without applying them. To run this mode use --check option
  - Suppose we've nginx.playbook which installs nginx on hosts. Ro run it we use --check option. Here ansible will not actually install nginx on hosts. Here in output we can see it changes state of webserver
  - Command :- **nginx.yml --check**

  ![image](https://github.com/user-attachments/assets/25f8a296-60d8-404f-866d-904624b6fcaa)

- **Diff mode** :- Diff when used with check mode shows difference between current state and after state of playbook run so that we can understand and verify impact of playbook changes before applying. Uses --diff option
  - Suppose we've to configure nginx and have playbook to ensure specific line is present in cfg file. Here in output we can check exact change made.
  - Command :- configure_nginx.yml --check --diff

  ![image](https://github.com/user-attachments/assets/55349835-1ea1-4f5b-a892-627c1e8f309c)


- **Syntax Check Mode** :- Ensures playbook syntax is error free and catch errors. Use --synatx-check option
  - Command :- **nginx.yml --syntax-check**
 
  ![image](https://github.com/user-attachments/assets/4ace3fca-a2ec-4a69-a3c3-4773e0cabea4)

  - If we've error in yml, we get error in output

  ![image](https://github.com/user-attachments/assets/013b7a8a-25d5-4a28-a539-db1a77bfaae4)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible-lint
-
- As a DevOps engineer we use Ansible to automate infrastructure in our organization and we've written multiple playbooks.
- As per the expansion of infra, playbook complexity also increases. So playbooks become more difficult to maintain and understand by others.
- To ensure consistency and quality across all playbooks, we need a mechanism. So "Ansible-lint" is used.

- It is a command line tool that performs linting on ansible playbooks, roles and collections. It checks lour code for potential errors, bugs, stylistic errors and suspicious constructs

- Suppose our playboook has some tasks to install and configure nginx but it contain some style related issues like inconsistent indentation, inconsistent task names

![image](https://github.com/user-attachments/assets/0ed0be70-414f-428b-8dd4-e08290a008f8)  

- When we run ansible-lint, we get below :- **ansible-lint nginx.yml**
  - From this we can refine our playbook
![image](https://github.com/user-attachments/assets/37264f96-c440-41cd-82f8-12d384d6f11c)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  

