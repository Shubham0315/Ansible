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
- Its present at :- /etc/ansible/hosts
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

------------------------------------------------------------------------------

