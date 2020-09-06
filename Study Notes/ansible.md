# Ansible

## Ansible help

> ansible -h

---

## Running pinging myservers

> ansible myservers -m ping

The -m stands for module

## Roles

A role is a downloadable component that you can install in your ansible system and it has all the ingredients you need to do simple and complex orchestration.
It's developed by the community and it's for executing in the ansible environment.

## Plugin

A plugin extends the functionality of what ansible can does.

You can create groups and name them:

[group_name_1]
host1
host2

[group_name_2]
host3
host4

You can do work in [all] groups and/or specific ones.

## Notes

Instead of setting configuration options while running commands, put the configuration in ansible.cfg and on the playbooks themselves for specific tasks.

Ansible is declarative, we tell them how to servers should not, not how to get to that point.

To let ansible know to pick another host file:

> ansible localhost -m ping -i new_other_host_file.txt

### Becoming another user before running command

> ansible my_host -m apt -a 'name=vim state=present' -b -K

Using module apt, and making sure vim is present.
-K is so it requests a password for the user.

### Executing commands on remote hosts:

> ansible hostname -a 'echo hello'

If not using -m, it uses by default the shell module

> ansible hostname -m shell -a 'echo hello'

With a module, but in this case is not necessary.

### Telling ansible to connect as a specific user

ansible -i hosts.txt webservers -m ping -u other_user

Where -u specifies the other user

## Common Modules

ping
shell

## Playbooks in yaml files

```yaml
---
- hosts: my_host # all, host_group, etc
  # Or put become:true here to be able to run all the tasks with this option
  become: true # To become superuser
  # remote_user: another_user
  tasks:
    - name: install vim
      apt: name=vim state=present
      # become: true
    - name: say hello
      shell: echo hello
    - name: stop nginx
      service: name=nginx state=stopped # started, etc
    - name: Install apache2
      apt: name=apache2 state=present update_cache=true
      notify: # This will call the 'Restart server' handler once apache2 is installed. Only runs when this task runs. If it's already installed, will not run.
        - "Restart server"
  handlers:
    - name: Restart server
      service: name=apache2 state=restarted
```

And run with

> ansible-playbook tasks.yml
