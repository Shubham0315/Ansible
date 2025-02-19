Ansible Playbooks
-

- Ansible playbooks are orchestration language for ansible as we define what tasks to perform in form of set of instructions.
- These instructions can be running commands on servers and restarting those servers in specific order
- It can be as complex as deploying 100s of VMs on public and private cloud, provision storage to VMs, setting up their network config, configuring apps on them, setting up LB, setting up monitoring , etc

- Ansible playbooks are collection/combination of plays where in each play there are fields like host (on which host of inv file this play execute), variables, remote user (using which user should the play execute on managed nodes), tasks (collection of things to be executed on target servers). Within each task we provide module

- Once we write this playbook, it is fed as input to control node where ansible is installed which then performs action on managed nodes
  - Command :- **ansible-playboook -i inv_file playbook.yml**
  - Ansible reads plays and execute the tasks as per servers in playbook
  - If we mention hosts as all (hosts: all) play will execxute on all nodes in inv file. If we define group (hosts: group_name), it will do accordingly

- All playbooks are written in yaml format. Play means set of tasks to be run on single or group of hosts. Task is an action performed on host like executing command, running shell script, install package, restart,etc.

- Below is example of playbook to perform activities on localhost

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
  
Ansible Conditionals
-
- Suppose we've 2 playbooks doing same task to install nginx on host but diff OS use diff package managers (for debian -apt and redhat -yum). As these are sepaarte playbooks we've to use right hosts for respective playbooks.

![image](https://github.com/user-attachments/assets/81ac5f8c-5d45-4c94-bd1c-6a87bef825c7)

- But what if we've to create single playbook for both of the OS for all hosts. Based on OS our playbook will run respective task. Here we can use conditional statements
  - We can use "when" to specify condition to run specific task so only if condition is met the task is executed
 
  ![image](https://github.com/user-attachments/assets/8b321d84-49e3-4675-8e64-06ce252925c8)

  - Condition can be any check that we perform just like "ansible_os_family" to check OS. Here we've to use == to check condtion
 
  ![image](https://github.com/user-attachments/assets/2c979486-1577-4626-bfe9-e76c33885d4c)

  - We can use "or" operator to use either of 2 conditions. Use "and" operator to satisfy both conditions
 
  ![image](https://github.com/user-attachments/assets/11ff0a36-d4b5-4e2c-a3f5-a5d790fe9d7b)

- We can use condtionals in loops as well. Like instead of sinhle package we've to install list of packages
  - Here we've array named "packages" to have list and property as below
  - First we specify loop directive to execute the install task in a loop, name of package to be installed is "item.name"
 
  ![image](https://github.com/user-attachments/assets/d0fc79c3-f0c0-4634-b57b-2ff771979962)

  - If we expand the loop we can see the loop is in 3 diff packages, each task having variable called "item" which has respective package details
  - So while writing condtionals, we can define item.required=true

  ![image](https://github.com/user-attachments/assets/0cc4e375-e24c-4d88-9dae-5393872a107c)
  ![image](https://github.com/user-attachments/assets/0d0d8fe2-642a-4de5-a64f-5e5bafc1949a)

- To use conditionals with output of a previous task we've to develop a playbook to check service status and trigger mail if service is down (2 task play)
  - Here to record 1st task o/p, we can use "register" directive :- **register: result**
  - In 2nd task we can use "when" conditional on that result variable of 1st task to state if result is down . Find method looks for string within variable and resturns its position, if not found it returns -1 as below.
  - That means if there is output not equal to -1, send email
 
  ![image](https://github.com/user-attachments/assets/5383b69e-484d-420c-b79e-140acf3224aa)

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible conditionals based on Facts, Variables and Re-use
-
- Suppose our organizatioon have a mix of diff servers of ubuntu, centos and windows. We've to automate deployment of web app across all servers
- Here playbook might need to perform diff sets of actions for diff servers
- Suppose we only have to install nginx on Ubuntu servers with 18.0 version. To ensure OS version running on server. Here we can use ansible-facts
  - Facts are system specific variables that are used in playbooks. They collect info about servers during execution of playbook
 
![image](https://github.com/user-attachments/assets/51bd6fb9-537c-4c49-a127-887436b939fa)

- Suppose our web app have diff config requirements based on env like dev, staging, prod end. We can define variable "app_env" to specify env and use it to deploy appropriate config file for specified env. It is using conditionals on variables

![image](https://github.com/user-attachments/assets/e4f79df4-e544-45d9-aeb9-b878d19efeef)

- Suppose we've common set of tasks to be performed on all servers like install package, create dir and give permissions
- But here we want to start web app service only on servers in prod. We can define variable "environment" and use it in conditional for our condition. It is conditional usage for reuse.

![image](https://github.com/user-attachments/assets/1f019a5e-a77a-4993-b43f-8d80d6555b76)


-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible Loops
-
- Suppose we're creating ansible playbooks to create users and assist them using "user" module which is used to create users on target systems
- But what if we've to create multiple users. We can have single task to loop over all the users. Thats where we use loops.
- Loop is a looping directive that executes same task multiple no of times each time it runs. It stores the value of each item in a loop in variable named "item".
  - So we can replace name by "item" variable as shown

  ![image](https://github.com/user-attachments/assets/80243ae9-79fd-454e-bb1a-52f01a77e024)

  - Here we dont repeat lines of user module or state
  - We can visualize loop like below for better understanding

  ![image](https://github.com/user-attachments/assets/3370011f-e887-4b7a-9b08-00c9144b8ebf)

  - Lopp breaks down into multiple tasks and within each task we've variable defined as "item" and each item has value from the list
  - Here loop is an array of string values, just usernames in above case
  - What if we've to specify user id as well. So each item in loop will have 2 values username and user ID

  ![image](https://github.com/user-attachments/assets/c7429997-5d57-42be-8b17-a50326ccbfb9)

  - Here how we can pass 2 values in array? So instead of passing an array of string to the loop we'll pass in array of dictionaries. Each disctionary will have 2 key value pairs. Keys will be name and ID and values will be name and IDs of each user
  - But now what we can use inside our task? We cannot use "item". As each task uses same module and parameter. We can see item variable inside each task in loop is a disctionary which has name and uid of each user.
  - So here we can do "item.name" and "item.uid" which we can define in task section
  - **In array of dictionaries we can use "array.propertyName"

  ![image](https://github.com/user-attachments/assets/4389bdcb-f051-4ee0-b01f-43b0522022a2)


  - Loop directive is used to create simple loops that iterate over a lot of items
 
- Another way to create loops is using "with_" directive

![image](https://github.com/user-attachments/assets/a093856d-9258-47d6-a9c5-acf64762871e)

  - With_items directive just iterates over a list of items. With_file directive iterates over multiple files and like that
