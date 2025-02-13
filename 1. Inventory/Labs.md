# Problem Statement

In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

A. student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.

B. node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:
- User: bob
- Password: caleston123

C. node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:
- User: bob
- Password: caleston123

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

1. Which of the following formats this inventory is using?
- web ansible_host=webserver.com
  db ansible_host=dbserver.com
- ini format

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2. Which of the following ports Ansible uses by default to connect to the Linux remote hosts?
- 22

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3. Which of the following inventory parameters can be used to establish a local connection instead of ssh in Ansible?
- ansible_connection

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4. What value we must set for ansible_connection parameter to connect to a Windows server?
- winrm

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

5. We have a sample inventory file called inventory under /home/bob/playbooks directory. It has 3 servers listed, add another server called server4.company.com in this file.
- ![image](https://github.com/user-attachments/assets/d31fea83-5c1a-442d-b7ed-b7e1b6d150af)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6. We have reset the /home/bob/playbooks/inventory inventory file, and added the aliases named web1, web2 and web3 for the first three hosts respectively. Update this inventory file to add an alias called db1 for server4.company.com host.

- ![image](https://github.com/user-attachments/assets/176559c8-cd80-4e54-890c-d90cb3bf340d)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

7. Update the inventory /home/bob/playbooks/inventory to add a similar entry for server4.company.com host. Find the required details from the table below.

|  Alias |        HOST         | Connection | User          | Password     | 

|  web1  | server1.company.com |    ssh     | root          | Password123! |

|  web2  | server2.company.com |    ssh     | root          | Password123! |

|  web3  | server3.company.com |    ssh     | root          | Password123! |

|  db1   | server4.company.com |    winrm   | administrator | Dbp@ss123!   |


- ![image](https://github.com/user-attachments/assets/af85c772-0302-471e-944c-d57d9f6d0784)
- ![image](https://github.com/user-attachments/assets/28f5dbfa-80c1-44b7-be3d-c8f78bb83019)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

8. We have updated the /home/bob/playbooks/inventory file and added a group called web_servers for web servers. Similarly, add a group called db_servers for database servers.

- ![image](https://github.com/user-attachments/assets/4a3a9bf6-bee6-4165-92b1-e9c21d37df39)
- ![image](https://github.com/user-attachments/assets/7a10ed44-ae6d-494f-8f62-3680d7222153)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

9. Let us now create a group of groups. Create a new group called all_servers and add the previously created groups web_servers and db_servers under it.

- ![image](https://github.com/user-attachments/assets/63ab0dc8-836b-4fb3-a514-e41a4d598279)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

10. Update the /home/bob/playbooks/inventory file to represent the data given in the below table in Ansible Inventory format.


| Server Alias |  Server Name  |  OS    |     User      | Password |

| sql_db1      | sql01.xyz.com | Linux  |     root      | Lin$Pass |

| sql_db2      | sql02.xyz.com | Linux  |     root      | Lin$Pass |

| web_node1    | web01.xyz.com | Win    | administrator | Win$Pass |

| web_node2    | web02.xyz.com | Win    | administrator | Win$Pass |

| web_node3    | web03.xyz.com | Win    | administrator | Win$Pass |

Group the servers together based on this table (Parent child use case)


|    Group         |  Members                          |

|    db_nodes      |  sql_db1, sql_db2                 |

|   web_nodes      |  web_node1, web_node2, web_node3  |

|    boston_nodes  |  sql_db1, web_node1               |

|    dallas_nodes  |  sql_db2, web_node2, web_node3    |

|   us_nodes       |  boston_nodes, dallas_nodes       |


- ![image](https://github.com/user-attachments/assets/45fd1f99-ba35-4a47-aa16-c9cd2b96d1ff)
