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

