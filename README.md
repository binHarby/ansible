## *Lecture 4*
1.	cloned our ansible git repo to `~/Devops/` + renamed file to Ansible
2.	pushed to the repo
3.	made a file named inventory in `~/Devops/Ansible`, added all the vms ips to it (bridge-adapter
  config)

#### Cmd1: 

``` bash
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
```
#### created & added to ansible.cfg at `~/Devops/Ansible`
```bash
#contents of ansible.cfg
[defaults]
inventory = inventory 
private_key_file = ~/.ssh/ansible
```
NOTE: `~/Devops/Ansible/ansible.cfg `overrides the default ansible config on `/etc/ansible`

#### Cmd2: 

```bash
ansible all -m ping 
```

#### Ouput:

```
osboxes@192.168.0.148 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
osboxes@192.168.0.145 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
osboxes@192.168.0.135 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
```

#### Cmd3: 

```bash
ansible all --list-hosts
```
```
  hosts (3):
    osboxes@192.168.0.145
    osboxes@192.168.0.148
    osboxes@192.168.0.135
```
#### Cmd4:
```bash
ansible all -m gather_facts 
```
#### Cmd5:
```bash
ansible all -m gather_facts  --limit <ip_addr>
```

## Lecture 5

#### Cmd6:

```bash
ansible all -m yum -a "name=epel-release state=latest" --become --ask-become-pass
```
*NOTE: check for each package options (in this case yum) for options of what you can do with each of them*

## Lecture 6:

Writing our first playbook
#### First Playbook

```yaml
---

- hosts: all
  become: true
  tasks:
  - name: update repo index
    yum:
      update_cache: yes
  - name: install httpd package
    yum:
      name: httpd
      state: latest
```
#### Second Playbook

```yaml
---

- hosts: all
  become: true
  tasks:
  - name: update repo index
    yum:
      update_cache: yes
  - name: removing httpd package
    yum:
      name: httpd
      state: absent
```
## Lecture 7

Covered the When conditional, we used when:ansible_distribution=="CentOS", check playbook for more details

