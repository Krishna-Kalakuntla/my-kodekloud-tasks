There is some data on all app servers in Stratos DC. The Nautilus development team shared some requirement with the DevOps team to alter some of the data as per recent changes they made. The DevOps team is working to prepare an Ansible playbook to accomplish the same. Below you can find more details about the task.

Write a playbook.yml under /home/thor/ansible on jump host, an inventory is already present under /home/thor/ansible directory on Jump host itself. Perform below given tasks using this playbook:

We have a file /opt/sysops/blog.txt on app server 1. Using Ansible replace module replace string xFusionCorp to Nautilus in that file.

We have a file /opt/sysops/story.txt on app server 2. Using Ansiblereplace module replace the string Nautilus to KodeKloud in that file.

We have a file /opt/sysops/media.txt on app server 3. Using Ansible replace module replace string KodeKloud to xFusionCorp Industries in that file.

Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure the playbook works this way without passing any extra arguments.

```
vi ansible/playbook.yml
```
Paste the below code and run ansible-playbook -i inventory playbook from ansible directory.

```

---
- name: File replace
  hosts: all
  become: true
  tasks:
    - name: Replace on app server 1
      replace: 
        path: /opt/devops/blog.txt
        regexp: 'xFusionCorp'
        replace: 'Nautilus'
      when: ansible_hostname == 'stapp01'
    - name: Replace on app server 2
      replace: 
        path: /opt/devops/story.txt
        regexp: 'Nautilus'
        replace: 'KodeKloud'
      when: ansible_hostname == 'stapp02'
    - name: Replace on app server 3
      replace: 
        path: /opt/devops/media.txt
        regexp: 'KodeKloud'
        replace: 'xFusionCorp Industries'
      when: ansible_hostname == 'stapp03'


```