One of the DevOps team members has created an ZIP archive on jump host in Stratos DC that needs to be extracted and copied over to all app servers in Stratos DC itself. Because this is a routine task, the Nautilus DevOps team has suggested automating it. We can use Ansible since we have been using it for other automation tasks. Below you can find more details about the task:
We have an inventory file under /home/thor/ansible directory on jump host, which should have all the app servers added already.
There is a ZIP archive /usr/src/security/xfusion.zip on jump host.
Create a playbook.yml under /home/thor/ansible/ directory on jump host itself to perform the below given tasks.
Unzip /usr/src/security/xfusion.zip archive in /opt/security/ location on all app servers.
Make sure the extracted data must has the respective sudo user as their user and group owner, i.e tony for app server 1, steve for app server 2, banner for app server 3.
The extracted data permissions must be 0644
Note: Validation will try to run the playbook using command ansible-playbook -i inventory playbook.yml so please make sure playbook works this way, without passing any extra arguments.

```
vi ansible/playbook.yml
```
Paste the below code, save and exit.
Run ansible-playbook -i inventory playbook.yml from playbooks directory.
```

---
- name: Unarchive zip
  hosts: all
  become: true
  tasks:
  - name: Unarchive task
    ansible.builtin.unarchive:
      src: /usr/src/security/xfusion.zip
      dest: /opt/security/
      mode: 0644
      owner: "{{ ansible_user }}"
      group: "{{ ansible_user }}"

```