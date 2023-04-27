# ansible-play
*Points to remember*
* Use `remote_src` for remotely copying files
* Use `lineinfile` when there is already file present in the targeted system 
* Cant use jinja with conditional statement in ansible playbook

### Example `roles`:
Create an Ansible role called package under /home/bob/playbooks/roles directory on student-node. It should install a package called nginx and should start its service as well.

Further consume this role in /home/bob/playbooks/role.yml playbook so that this role can be applied on node01

SOLUTION:
Run below commands:

```bash
cd /home/bob/playbooks/roles/
ansible-galaxy init package
vi /home/bob/playbooks/roles/package/tasks/main.yml
```


Add below code in this task:

```yaml
---
# tasks file for nginx
- name: Install Nginx
  ansible.builtin.package:
    name: nginx 
    state: latest
- name: Start Nginx Service
  ansible.builtin.service:
    name: nginx 
    state: started
```


Now modify the /home/bob/playbooks/role.yml playbook so that it looks like as below:

```yaml
---
- hosts: node01
  become: true
  roles:
    - roles/package
```

