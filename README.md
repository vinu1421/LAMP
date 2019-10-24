# Installing LAMP Stack using ansible

## Prerequisite:
   
   Create an inventory file with proper host added.


## **lamp.yml**

```

---
- name: "To install LAMP Stack"
  hosts: all
  become: yes
  tasks:

   - name: "LAMP - Install apache,mariadb,php"
     yum:
      name:
              - httpd
              - mariadb-server
              - php
      state: present

   - name: "LAMP - Adding some PHP file"
     copy:
      content: "<?php phpinfo(); ?>"
      dest: /var/www/html/index.php

   - name: "LAMP - Adding some html file"
     copy:
      content: "<h1> Testing </h1>"
      dest: /var/www/html/index.html

   - name: "LAMP - Restarting/Enabling services"
     service:
      name: "{{ item }}"
      state: restarted
      enabled: yes
     with_items:
             - httpd
             - mariadb
```

