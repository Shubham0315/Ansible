Variables
-
- Used to store values that varies with different items
- Suppose we've to perform same operation applying patches to 100s of servers. We only need single playbook for all 100 servers. However variables store the info about diff hostnames, usernames, passwords for each server.

- We've already checked variables in inventory file section

![image](https://github.com/user-attachments/assets/c594bd4d-01d0-4b1a-90a8-4727b58e3f4c)

- We can also define variables inside playbook by defining "vars" directive followed by key value pair

![image](https://github.com/user-attachments/assets/c2cc479c-2080-4759-85bb-4866461fe4da)

- We can also have separate file dedicated for variables

![image](https://github.com/user-attachments/assets/6d39cd30-4c0e-437f-9cee-44411f3e9212)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

How to use variables?
-
- Previously we've defined variables but havent used them. If we've defined variable as server : 10.10.10.10 we can use them without hardcoding them. Use them inside curly braces. So when we run playboos, ansible will replace it with value

![image](https://github.com/user-attachments/assets/01ae7b32-e486-4de1-ac85-5e5f54323ec8)

- In other case if we define values of variables inside our playboos, everytime we have a change we've to modify the values in entire playbook which can be errorprone. So we can define values of variables in inventory file and use them as reference in our playbook so not to modify playbook.

- Another way can be to move the variables into file in the name of host. All values defined in this file are available to use by playbook when run on that host.
  - Here we've host as "web". PFS

  ![image](https://github.com/user-attachments/assets/28c250dc-ec68-4f0f-b77c-8cb85941bb3e)

** This format to use variables in playbook is called :- Jinja2 templating

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Variable Types
-

1. String Variables
- Sequences of characters. They can be defined in playbook, inventory or passed in as command line arguments
- e.g :- username: "admin"

2. Number Variables
- Can hold integer or floating point value. Can be used in mathematical operations
- e.g :- max_connections: 100

3. Bollean Variabke
- True or false. Often used in conditional statements
- e.g :- debug_mode: true

4. List Variables
- Holds ordered collection of values. Values can be of any type

![image](https://github.com/user-attachments/assets/dbdc2c8b-fa3b-413f-9aad-7e7794a0ad6f)

5. Distionary Variables
- To hold collection of key-value pairs. Key and values can be of any type
- We can reference those in playbooks using double curly brackets

![image](https://github.com/user-attachments/assets/550b9571-69d2-4c2f-8f08-f655de385fd1)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Registering variables and Variables' Precedence
-
- If we've variable defined in 2 different places. We've variable defined for each host in our group of hosts and all of them have same dns_host where we can define dns_server variable with IP of that (done within /etc/ansible/hosts file)
- WEhen playbook is run, ansible creates host objects in memory. Then it identifies which group each host belong to and then associates group variables to each host

![image](https://github.com/user-attachments/assets/802382d9-312d-41a7-818e-0ffba0c55324)

- What if we define same dns_server variable on host as well for one of the host, dns_Server IP is other. So while running playbook, ansible will first associate group variables and then host variables. So variable defined at host level will go to that server. That is variable precedence
- Host variables takes precedence over group variables

![image](https://github.com/user-attachments/assets/72ea9b38-d851-40cf-9416-4044461d25de)

- For variables defined in playbook, if we've defined same variable in host level, group level and play level, whatever we defined at play level overrides others

![image](https://github.com/user-attachments/assets/7dc63677-a7ea-4689-8c18-7a8a8b01df3d)

- We can also run the extra variable using --extra_vars option which takes highest precendece (used as CL arguments)
- Command :- **ansible-playbook playbook.yml --extra_vars "dns_server-1.1.1.1"**


- Sometimes we need to store output of one task and use later. Lets bring o/p of /etc/hosts on server. Also print output of first command using debug module
  - We can use "register" directive in playbook with first command and specify variable name so output will be captured into that variable. Specify same variable in var option of debug module as shown below

  ![image](https://github.com/user-attachments/assets/88222efb-a9da-4fce-90cd-7617065249dd)

  - Now data stored in variable depends entirely on what module was run. So we get below output for above case

  ![image](https://github.com/user-attachments/assets/3fea0ca5-3e21-4b68-b7cf-9b2875349914)

- Any variables created using "register" directive falls under scope of that host. So we can use them in another plays as required in same playbook.

- Another option to view output of task if we dont want to use debug module, is passing -v option in CL arguments
- Command :- **ansible-playbook -i inventory playbook.yml -v**

![image](https://github.com/user-attachments/assets/aefeb71e-13f5-445e-8f94-23d89f0eb2fa)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Variable Scoping
- In single inv file, we've dns_server specified for host "web2" . As scope defines accessibility or visibility of variable, variable is accessible by knowing how and where it is defined

![image](https://github.com/user-attachments/assets/28e02ba3-b021-4584-87ff-24d0e30b1583)

1. **Host Scope**
- Varible defined as host varaible is accessible within play that is run for that host. We can define theis variable in inv file or part of group variable. Ultimately when ansible playbook is run, it breaks down groups and associates variables with hosts. So when playbook is run, there is just one scope "Host Scope"

2. **Play Scope**
- If we've defined value of variable only in first play but it will not be accessible in 2nd play due to scope

![image](https://github.com/user-attachments/assets/6b8cd953-5063-4a2c-94d0-607f38c3bb85)

3. **Global Scope**
- When we define using CL arguments

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Magic Variables
-
- When ansible playbook starts, it creates sub processes for each host in inv file. During variable interpolation, it takes variables from inv file and associates them with repsective hosts. Just like dns_Server IP will be unavailable on web1 and web3 as below

![image](https://github.com/user-attachments/assets/7a1f08f0-19ef-44ec-8900-0e6c3a7b75f6)

- To get dns_Serevr IP on web1 and web3, we can use "Magic Variables"

1. **Hostvars**
  - We can use magic variable "hostvars" to get varaibles defined on another host

  ![image](https://github.com/user-attachments/assets/460064ab-6fdd-460d-be1c-6b79a517de54)

  - We can use for other details as well

  ![image](https://github.com/user-attachments/assets/cf43ac33-1567-4059-ae42-efcbe42b5dab)

2. **Groups**
  - Returns all hosts under given group

  ![image](https://github.com/user-attachments/assets/edb1797e-53e5-4510-b0eb-03b796c348bf)

3. **group_names**
  - Returns all groups current host is part of

  ![image](https://github.com/user-attachments/assets/4ac64709-84ff-4b9b-9be9-be7a5971c632)

4. **inventory_hostname**
  - Gives name configured for the host in inventory file

  ![image](https://github.com/user-attachments/assets/9b458863-5f74-4dd6-9ca2-b848cb91c1b8)

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ansible Facts
-
- When we run playbook and ansible connects to target machine, it collects all info of machine like OS, processor, memory, host,networks, IP. They are facts
- Ansible gathers all these facts using "setup module". Setup module is run auto by ansible to gather facts about host when run even if we dont use this module in playbook.

- Suppose we've to onluy print message means just one task using debug module. When we run playbook we see it run 2 tasks. First to gather facts and 2nd to print.

![image](https://github.com/user-attachments/assets/84a35c4e-5758-4616-82fd-016278e3ae88)

- All facts gathered by ansible are stored in variable "**ansible_facts**"

![image](https://github.com/user-attachments/assets/a288d6fe-efaa-420a-a05b-9ff347a69a33)

- If we dont want ansible to gather facts, means to disable gathering facts, we can do that using "gather_facts: no" in our play. So we can see only single task of printing.

![image](https://github.com/user-attachments/assets/ce3c64e0-0724-4a32-b688-36d4bc026144)

- Behavior of gathering facts is governed by setting in ansible cfg file called "**gathering**" (explicit/implicit)

![image](https://github.com/user-attachments/assets/80a0546f-bfed-4cae-96d0-161cc9e8cf6e)

- If we havent specified gathering facts neither in playbook nor in cfg file, setting in playbook takes precedence.

- Ansible only gathers facts about hosts that are part of playbook. Lets say we've inv file with 2 hosts but playbook targets only 1 host, so facts will be gathered only for that 1 host in playbook

![image](https://github.com/user-attachments/assets/9e418c78-5830-4014-ab8a-53ff90fc79b0)
