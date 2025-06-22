# Ansible

- Ansible is an open source automation tool used for config management, app deployment and orchestration. It ensures users to automate tasks across multiple systems efficiently without requiring installation of agents on managed nodes

Features of Ansible
-
- Automation tool to simplify repetitive tasks
- **Agentless architecture** :- uses SSH, winrm to communicate between machines, no software required to install on target machines. Reduces overhead and simplify security
- **Declarative approach** :- uses yml files *playbooks) to define desired state of systems
- **Cross-platform** :- work acorss diff OS like linux, windows and even cloud
- **Scalability** :- can handle large scale deployments
- **Idempotency** :- ensures tasks are only executed when required, avoiding repeated actions

Ansible Architecture
-
- Control Node
  - Machine where ansible is installed and executed
  - Manages entire automation process by sending tasks (defined in playbook) to managed nodes
  - Requires python installed and uses SSH/winRM to communicate with managed nodes
 
- Managed Nodes
  - It is any system that ansible configures, deploys app on or performs tasks for
  - No agent is required, only SSH/winRM must be enabled
  - These nodes are listed in inventory file on control node
 
- Control node sends instructions and managed nodes execute them enabling efficient automation across multiple systems

------------------------------------------------------------------------------

Ansible vs Shell script vs Python
-
- We can write shell script on control node and execute. If some of our control nodes are windows and some are linux, shell script wont do execution on windows machines
- We can use python to get it worked on all types of VM. But we need python knowledge as well as we need to maintain code by logging to VM timely
- Here ansible works. We dont need to login VM. We just need to install ansible on control node which reads inv file having server info of managed nodes and performs required tasks. No manual intervention is needed.

- Use absible for infra automation, config management
- Use shell for quick , simple system level tasks
- Use python for advanced logic, API integrations and tasks requiring flexibility

------------------------------------------------------------------------------

Install Ansible on Ubuntu EC2
-
- Create EC2 ubuntu instance. Ensure SG allows SSH access
- Connect to EC2
- Switch to root :- **sudo -i**
- Update package list :- **apt update**
- Install python :- **apt install python3 -y**
- Install ansible :- **apt install ansible -y**
- Verify :- **ansible --version**

------------------------------------------------------------------------------

Ansible passwordless authentication
-
- Enables ansible to communicate with managed nodes without prompting for a password. 
- Commonly achieved using SSH key-based authentication which simplifies secure communication between ansible controller and managed hosts
- SSH key authenticationuses key pair :- private key kept securely on control node, public key added to ~/.ssh/authorized_keys file on managed hosts
- Once set up, it allows you to login to remote machines witjout entering password each time

- Steps :-
  - Generate SSH key pair :- **ssh-keygen -t rsa -b 2048**. Save key in ~/.ssh/id_rsa
  - Copy public key to managed hosts :- **ssh-copy-id user@managed_host**. Adds public key to ~/.ssh/authorized_keys file on remote host
  - Test passwordless SSH access :- **ssh user@managed_host**
 
------------------------------------------------------------------------------

Ansible Inventory
-
- File that lists managed nodes where ansible has to automate infrastructure on. Its present on control node
- It tells ansible which machines to manage and provides config info of those machines
- Its present at :- /etc/ansible/hosts   (hosts is name of file)
- Typically present in INI or YAML formats
- It supports grouping of hosts or mark individual hosts

- 2 types :- static and dynamic

[webservers]
web1.example.com
web2.example.com

or

[databases]
db1.example.com ansible_user=dbadmin ansible_port=2222

------------------------------------------------------------------------------

Ansible ADHOC commands
-
- Used to run quick and one time tasks without writing playbook
- Ideal for quick verifications or one-off tasks
- Ping all managed nodes :- **ansible all -m ping**
- Check disk space on all servers :- **ansible all -m shell -a "df -h"**
- Install package on web servers :- **ansible webservers -m apt -a "name=nginx state=present"**


- If we define our inventory other than hosts suppose inventory.ini and want to ping :- **ansible -i inventory.ini -m ping all**

------------------------------------------------------------------------------

Playbook
-
- Its written in YML language. YML is human readable data serialization format often used for config files and data exchange
- It uses indentation in structured format
- Playbook defines what tasks ansible should perform on which hosts
- Playbook consist of :-
  - **Plays** :- which hosts to target and in which order
  - **Tasks** :- what to do like install, copy, restart
  - **Modules** :- building blocks used in tasks (yum, copy, service)

------------------------------------------------------------------------------

Ansible Role
-
- Ansible role is a reusable, self-contained unit of automation that is used to organize and manage tasks, variables, file, templates and handlers in structured way.
- Roles help to encapsulate and modularize logic and config needed to manage system or application component
- This modular approach promotes reusability, maintainability and consistency across different playbooks and environments

![image](https://github.com/user-attachments/assets/3cbf6c56-0b2f-4e38-9d1d-3225549de75c)

- In above
  - Files :- are static files we can copy on remote hosts using copy module
  - Templates :- Files using Jinja2 Templating language to enable dynamic content generation.

![image](https://github.com/user-attachments/assets/784abbb4-d0b2-43b8-83a8-911cfd690f9a)

- To create role manually using command :- **ansible-galaxy init webserver**

- **Modularity** :- Roles allow to break down complex playbooks into smaller, reusable components. Each role handles specific part of config
- **Reusability** :- Once created roles can be used across playbooks and projects saving time and effort
- **Readability** :- Roles make playbooks cleaner and easier to read 

------------------------------------------------------------------------------

Ansible Galaxy 
-
- Its a community hub for finding, sharing, downloading and managing ansible roles and collections. It allows users to find prebuilt roles to automate tasks, saving effort and time
- We can use "ansible-galaxy" command to download or manage roles. Roles are reusable units of automation
- Command to install role from ansible galaxy into project :- **ansible-galaxy install username.role**
- To create/initialize role :- **ansible-galaxy role init httpd**

- First we need to install role from galaxy and then define it in playbook and then run the playbook so that whatever is defined in roles get executed on our hosts

------------------------------------------------------------------------------

Ansible Handlers
-

![image](https://github.com/user-attachments/assets/aecebff9-f16e-4692-9d6c-2cff5e646721)

- Handlers are special tasks triggered by notify statements. Typically used to perform actions that should only run when there is a change in syatem such as restarting service after updating config file

- In playbook, define handlers. Trigger with notify. Run handler once per play.
- This mechanism ensures that changes requiring follow up actions are handled efficiently

------------------------------------------------------------------------------

Creating AWS resources using Ansible
-
- Ansible provides AWS collection which includes modules like ec2, rds, s3_bucket, and others to interact with AWS services.
- Pre-requisites :-
  - pip install ansible
  - pip install boto3 botocore
  - aws configure (configure creds and region)
  - ansible-galaxy collection install amazon.aws (ansible AWS collection to access AWS modules)
  - IAM roles access
 
- Write the playbook with all config for S3 or EC2

![image](https://github.com/user-attachments/assets/794f2408-87e6-4000-828b-7e8df75d5c1c)

- Run the playbook :- **ansible-playbook aws_resources.yml**
- Verify resources in AWS console

------------------------------------------------------------------------------

Ansible Vault
-
- Its an Ansible feature that allows you to securely store sensitive data like passwords, API keys or other credentials in encrypted files. It ensures sensitive information is not exposed in plaintext, even when stored in VCS
- Vault is to manage secrets in infrastructure automation workflows

- Features of Vault
  - Encryption and decryption :- encrypt sensitive files using password or key, decrypt files when needed for playbook execution or editing
  - Integration with Ansible :- used in playbooks, roles, variable files
  - Granular security

- Common Commands
-
- Create encrypted file :- **ansible-vault create file_name**
- Edit encrypted file :- **ansible-vault edit file_name**
- Encrypt existing file :- **ansible-vault encrypt file_name**
- Decrypt existing file :- **ansible-vault decrypt file_name**
- View encrypted content :- **ansible-vault view file_name**
- Change password :- **ansible-vault rekey file_name**

- If our playbook uses sensitive credentials, you can store password in file encrypted with Vault. During playbook execution, ansible auto decrypt file if correct password is provided, keeping creds secure

------------------------------------------------------------------------------

Variables in Ansible
-
- Variables allows to store and manage dynamic values like config parameters, credentials or env specific details which can be referenced and reused across playbooks, tasks, roles and templates
- We can define variables in playbooks, in inv files (static/dynamic), in variables files and reference them in playbooks, inside facts

- Variable precedence :- If variable is defined at multiple places, one with highest precedence will be used (Highest to lowest)
  - Command line options - Task level - Role defaults - Play - Inventory - Facts
 
- Variables can be string, integers, boolean, dictionaries

------------------------------------------------------------------------------

