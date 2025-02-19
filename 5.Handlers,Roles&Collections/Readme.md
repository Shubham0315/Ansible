# Ansible Handlers

- In ansible, handlers are special tasks that are triggered only when notified by other tasks. They're used to perform actions that should occur when there is a change in syatem state, such as restarting a service after config file is modified.

- Suppose we've a website and we want to update its content. Our playbook will just update the HTML file on our server to update content of website. Nut here the requirement is we've to restart the application server after updating HTML.
- So updated content reflects on our website

- Process :-
  - Copy updated HTML onto app server
  - Restart the app server

- To use these tasks, we need ansible handlers
- Here we can use "notify" handler for task which we need to do. Here we specify "restart nginx" as we've already updated the HTML
- We also need to use attribute "handler" inside which we can write task to restart our server

![image](https://github.com/user-attachments/assets/bcfd1182-e434-4d51-ac36-e88eb29173e4)

- Key Features :-
  - Triggered by notification :- Handlers run only when they're notified by another task. This is useful for avoiding unnecessary actions (avoiding service restart incase of no config change)
  - Executed once :- If multiple tasks notify the same handler, it will be executed only once after all tasks are completed
  - Run at the end :- Handlers are executed at the end of play after all tasks are completed.
 
- Suppose we want to update Nginx config file and restart Nginx service only if file was changed

![image](https://github.com/user-attachments/assets/c20617ac-643d-4e44-ac46-a1deffe0c3bc)

  - notify :- used in task to trigger handler if nginx.conf file changes
  - handlers :- defined at play level with "name" that matches the notification
  - handler use "service" module to restart nginx service

--------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Ansible Roles

- Suppose we've playbook with 50 tasks with multiple variables. We've task section where we've many tasks. Also have 50+ handlers
- Here size of playbook goes high. Here our playbook looses readability (if we've 2000 lines we will loose interest to read file)

- In our playbook, there are multiple sections now like tasks, vars, handlers. We can split these sections and put them in different folders and in each folder we've individual yaml files.
  - i.e create folders for tasks, vars, handlers
 
- This will enhance our readability and modularity. To address that ansible brings in concept of "ROLES"

- Role is nothing but take ansible playbook and split diff sections into diff folders and place them under one umbrella, it becomes role.

- **ansible-galaxy** :- command to create, manage, delete and list roles

- Syntax :- **ansible-galaxy role init $role_name**
  - We've vars, tasks, handlers, meta in our playbook. When we run above command, inside role_name folder, all these folders get created

![image](https://github.com/user-attachments/assets/270b211a-135d-45c2-a899-40c9e82538ec)

- Suppose we've to install and configure oracle. There will be so many steps to do so. Using roles we can make our playbook more readable, modular.

- Using ansible-galaxy we can create roles and upload them on github to share withon our organization

- We should go for roles for readability, modularity and sharing across teams

Different folders in Ansible Roles
-
- **vars** :- To place all variables. Inside this folder main.yml file we can define variables
- **tasks** :- Copy tasks in plays and inside this folder's main.yml file paste them
- **meta** :- About metadata like owner, author, version of role ,etc
- **handlers** :- Ansible tasks which we want to execute upon specific action.
  - Suppose in below we've 2 handlers - restart memcached and restart apache
  - In tasks section of below, we're copying file, we state restart apache

![image](https://github.com/user-attachments/assets/0c284e76-18fd-4751-bd1b-b2037d1bb81c)

  - Execute the handler only when we get request to do so
- **defaults** :- They are also variables but default values. If we dont provide value to vars we create by default it takes values present in default/main.yml
- **files**
  - Suppose we've multiple html files where our playbook is in GitHub. Instead inside files/ folder of roles, place those files and inside playbook.yml reference those files as files/index.html instead of just index..html
  - These are static files that we can copy to remote hosts using 'copy' module. Handlers are executed once notified that specific action is complete.

![image](https://github.com/user-attachments/assets/4fd930d3-0702-49c5-8b0e-19538b43781e)

- **templates**
  - Almost same to files. When we've dynamix files (need dynamic values) like changing ec2 name, use templates


Practical
-
- Suppose we've playbook, inv file and html file in dir and we've to convert the playbook into role.
- ansible-galaxy role init httpd :- creates httpd role and all folders inside role

![image](https://github.com/user-attachments/assets/c41ab4c9-e1b3-4b39-bc73-cd47d80c48f4)

- Inside playbook we only have tasks, remove tasks section from playbook and copy it. Go to httpd role, inside task folder, main.yml and paste there.
  - Below is playbook
  
![image](https://github.com/user-attachments/assets/7aba20c3-8683-4fc8-8acc-ed58ae79775a)

  - Below is role/tasks/main.yml. 

![image](https://github.com/user-attachments/assets/f9c63c32-8783-4328-bcdf-65366a7e4e18)

- Now how will the playbook.yml understand tasks are present inside role/tasks/main.yml or which role to use.
  - Go to playbook.yml. Define roles like below
  
![image](https://github.com/user-attachments/assets/f972494a-f96c-4a6c-be49-c2a052b30cf6)

- Move our index.html and paste in httpd/files. So that our dir will now have playbook, inv file, and httpd role
- Go to src section and update the location as files/index.html

![image](https://github.com/user-attachments/assets/60bab26e-7a66-472e-af98-658e9f53fa4f)

- Now to run our role :- **ansible-playbook -i inventory playbook.yml**
  - This will first gather facts. Then install apache. Then copy files
  - It shows 0 changed tasks as ansible is idempotent. If anything is already there on target, it will not execute again
 
![image](https://github.com/user-attachments/assets/efd9018e-7f05-4e05-a738-8042cf8d26f2)


