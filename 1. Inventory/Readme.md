- Ansible can work with one or multiple systems in our infrastructure at the same time. To do so ansible needs to establish connectivity with them. This is done using SSH for linux and powershell remoting for windows. This makes ansible agentless. Means we dont need to install any additional software on target machines to be able to work with ansible.

- Disadvantages with other orchestartion tools is we need to install agent on target machines to run any automation

- In ansible, info about target machines is stored in inventory file. If we dont create any inventory file, ansible uses default inventory file located at :- /etc/ansible/hosts

- Inv file is in ini format where servers are listed. We can also group different servers by defining group name in [] and under them list servers. We can have multiple groups in single file

![image](https://github.com/user-attachments/assets/02a490ec-609a-49d3-8438-1462de0b8e37)

- If we've 4 servers in inv file and we need to refer them using alias. We can add alias for each server at beginning of line and assign address of that server to **ansible_host** parameter. ansible_host is an inventory parameter used to specify IP address of server
  - There are other ansible inv parameters like
    - ansible_connection :- defines how ansible connects to target servers (ssh/winrm/localhost)
    - ansible_port :- defines which port to connect to (default is 22 port for ssh)
    - ansible_user :- defines user used to make remote connection (default is root for linux machines
    - ansible_ssh_pass :- defines ssh password for linux (passwordless authentication is recommended)

![image](https://github.com/user-attachments/assets/83168579-68a2-4a29-842c-f7379b8ceb2d)


Inventory Formats
-
- One is startup hosting web and db. Other is MNC with 100s of servers handling diverse functions.
- For startup basic inventory is needed while for MNC more detailed inventory. This is where YAML comes in where complex organizational charts with various departments and teams we can do.
- Here we can group servers based on roles like web, DB, app.

- Ansible supports 2 types of inventory formats
  - INI :- simplest, basic organizational chart for small startup
  
  ![image](https://github.com/user-attachments/assets/8284ead7-eab5-4bd0-b347-2afbff9c90df)

  - YAML :- More structured and flexible. Its like complex organizational charts for MNC

  ![image](https://github.com/user-attachments/assets/f2dd1778-954f-4c20-949e-c547416437f5)


Grouping and Parent-Child Relationships
-
- In large MNC we've 100s of servers spread across multiple locations serving diff tasks. If we need to update specific group of servers we've to manually specify each web server which can be timely and errorprone

- So to manage complex IT infrastructure, we can categorize servers based on their roles, locations or any criteria. We can label all "web" servers under specific label name, so to update we can target "web" label so changes will be applied to all servers associated with that label
  - This will save time and reduce errors
 
- So with "Grouping" we can create common labels/groups to manage set of servers

- If our web servers also are spread across locations, and they have location specific config.
- Here, We can create separate group for them for each location but it will lead to duplicate lot of common config
- So using parent-child relation, we can create parent group called "web" and child groups for each location "web-us", "web-eu". We can define common config at parent group level and location specific at child group level.

![image](https://github.com/user-attachments/assets/38a2f83a-fe3b-44cf-a5ac-65c5cd207925)

- This way we can manage our servers more efficiently and avoid configuration duplication

- In INI format, groups are defined using [] and hosts are listed under respective groups

![image](https://github.com/user-attachments/assets/3db99f08-b0bc-4afb-a4c3-d073c2e2aef2)

- Parent child relation is defined using :children suffix

![image](https://github.com/user-attachments/assets/e68c73fe-f5c6-4ded-b77f-4891402f0552)

