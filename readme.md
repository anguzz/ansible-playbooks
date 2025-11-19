# Ansible Playbook Examples

A collection of Ansible playbooks for labs, home/work automation templates, and graduate-level systems automation coursework.

## Repository Structure

```
ansible-playbooks/
│
├── README.md
├── ansible.cfg
├── inventory
│
├── playbooks/
│   ├── facts-dashboard/
│   │   ├── facts_dashboard.yml
│   │   ├── templates/
│   │   └── css/
│   ├── backup-manager/
│   │   ├── backup_manager.yml
│   │   └── vars/
│   └── ...etc
```



##  Running a Playbook

Run any playbook from the repo root:

```bash
ansible-playbook playbooks/<folder>/<playbook>.yml
````

Example:

```bash
ansible-playbook playbooks/facts-dashboard/facts_dashboard.yml
```

##  Notes

* Designed to work on localhost or remote hosts (update `inventory` accordingly).
* Playbooks will continue to be added over time as new examples and automations are created.
* Originally created for Ubunut/Debian based hosts


### Setup

```bash
sudo apt update
sudo apt install ansible -y
````

Use  `ansible all-m ping` to verify install.

```bash
angus@angusMintDev:~/Documents/GitHub/ansible-demo$ ansible all -m ping
[WARNING]: Platform linux on host localhost is using the discovered Python interpreter at /usr/bin/python3.12, but future installation of another Python interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-core/2.16/reference_appendices/interpreter_discovery.html for more information.
localhost | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3.12"
    },
    "changed": false,
    "ping": "pong"
}
```


### This line is just a warning (safe to ignore):

```
[WARNING]: Platform linux on host localhost is using the discovered Python interpreter...
```

It’s Ansible letting you know:

* It auto-detected Python at `/usr/bin/python3.12`
* In the future, if you install another Python version, it *might* use a different path

This does **NOT** break anything.
It’s strictly informational.

---

#  **The important part: SUCCESS**

```
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

This means:

* Ansible reached `localhost`
* The connection plugin worked (`local`)
* Python interpreter exists
* Modules can execute



# Runnng playbooks

 Now run:

### Facts dashboard playbook:

```
ansible-playbook playbooks/facts-dashboard/facts_dashboard.yml
```

### Backup playbook:

```
ansible-playbook playbooks/backup-manager/backup_manager.yml
```



