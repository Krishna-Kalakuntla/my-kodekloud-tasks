Task description

Several new developers and DevOps engineers just joined the xFusionCorp industries. They have been assigned the Nautilus project, and as per the onboarding process we need to create user accounts for new joinees on at least one of the app servers in Stratos DC. We also need to create groups and make new users members of those groups. We need to accomplish this task using Ansible. Below you can find more information about the task.

There is already an inventory file ~/playbooks/inventory on jump host.

On jump host itself there is a list of users in ~/playbooks/data/users.yml file and there are two groups — admins and developers —that have list of different users. 

Create a playbook ~/playbooks/add_users.yml on jump host to perform the following tasks on app server 1 in Stratos DC.

a. Add all users given in the users.yml file on app server 1.

b. Also add developers and admins groups on the same server.

c. As per the list given in the users.yml file, make each user member of the respective group they are listed under.

d. Make sure home directory for all of the users under developers group is /var/www (not the default i.e /var/www/{USER}). Users under admins group should use the default home directory (i.e /home/devid for user devid).

e. Set password B4zNgHA7Ya for all of the users under developers group and B4zNgHA7Ya for of the users under admins group. Make sure to use the password given in the ~/playbooks/secrets/vault.txt file as Ansible vault password to encrypt the original password strings. You can use ~/playbooks/secrets/vault.txt file as a vault secret file while running the playbook (make necessary changes in ~/playbooks/ansible.cfg file).

f. All users under admins group must be added as sudo users. To do so, simply make them member of the wheel group as well.

Encrypt the password

```ansible-vault encrypt-string <password> --vault-file-name=~/playbooks/secrets/vault.txt --name=<variable_name>```

Create add_users.yml in playbooks directory.

```vi /home/thor/playbooks/add_users.yml```

Paste the below code
```---
- hosts: <your appserver name>
  become: yes
  gather_facts: no
  vars:
    admin_pass: <output after running the ansible-vault command>
    dev_pass: <output after running the ansible-vault command>
  tasks:
    - name: create groups
      group:
        name: "{{ item }}"
        state: present
      with_items:
        - admins
        - developers

    - name: Include user.yml
      include_vars:
        file: /home/thor/playbooks/data/users.yml

    - name: Creating admins
      user:
        name: "{{ item }}"
        password: "{{ admin_pass | string | password_hash('sha512') }}"
        groups: wheel,admins
      with_items: "{{ admins | list }}"

    - name: creating developers
      user:
        name: "{{ item }}"
        password: "{{ dev_pass | string | password_hash('sha512') }}"
        home: /var/www
        groups: developers
      with_items: "{{ developers | list }}"
```

Add vault file parameter in ansible.cfg file.

```vi playbooks/ansible.cfg```

paste below text

```vault_password_file = /home/thor/playbooks/secrets/vault.txt```
    
