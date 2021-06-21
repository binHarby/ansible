## *lecture 4*
1.	cloned our ansible git repo to `~/Devops/` + renamed file to Ansible*
2.	pushed to the repo
3.	made a file named inventory in `~/Devops/Ansible`, added all the vms ips to it (bridge-adapter
  config)
cmd1: 

``` bash
ansible all --key-file ~/.ssh/ansible -i inventory -m ping
```
```
added inventory = inventory 
private_key_file = ~/.ssh/ansible
```
NOTE: this overrides the default ansible config on /etc/ansible
cmd2: 
```bash
ansible all -m ping 
```
Ouput:
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

cmd3: 
```bash
ansible all --list-hosts
```
```
  hosts (3):
    osboxes@192.168.0.145
    osboxes@192.168.0.148
    osboxes@192.168.0.135
```
