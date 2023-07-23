
The Nautilus DevOps team is practicing some of the Ansible modules and creating and testing different Ansible playbooks to accomplish tasks. Recently they started testing an Ansible file module to create soft links on all app servers. Below you can find more details about it.



Write a playbook.yml under /home/thor/ansible directory on jump host, an inventory file is already present under /home/thor/ansible directory on jump host itself. Using this playbook accomplish below given tasks:

Create an empty file /opt/sysops/blog.txt on app server 1; its user owner and group owner should be tony. Create a symbolic link of source path /opt/sysops to destination /var/www/html.

Create an empty file /opt/sysops/story.txt on app server 2; its user owner and group owner should be steve. Create a symbolic link of source path /opt/sysops to destination /var/www/html.

Create an empty file /opt/sysops/media.txt on app server 3; its user owner and group owner should be banner. Create a symbolic link of source path /opt/sysops to destination /var/www/html.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way without passing any extra arguments.

Create a playbook.yml under ansible directory and paste below code, validate the task.


```
---
- name: Symlink on servers
  become: true
  hosts: all
  tasks:
  - name: Create file on app server 1
    file:
      path: /opt/sysops/blog.txt
      owner: "{{ ansible_user  }}"
      group: "{{ ansible_user  }}"
      state: touch
    when: ansible_hostname == 'stapp01'
  - name: Create file on app server 2
    file:
      path: /opt/sysops/story.txt
      owner: "{{ ansible_user  }}"
      group: "{{ ansible_user  }}"
      state: touch
    when: ansible_hostname == 'stapp02'
  - name: Create file on app server 3
    file:
      path: /opt/sysops/media.txt
      owner: "{{ ansible_user  }}"
      group: "{{ ansible_user  }}"
      state: touch
    when: ansible_hostname == 'stapp03' 
  - name: Symlink on all app server 
    file:
      src: /opt/sysops/
      dest: /var/www/html
      state: link
```