
## Backup Manager

This playbook creates a timestamped backup of selected folders and compresses them into `~/backups`.

###  Run the Backup Playbook

```bash
ansible-playbook playbooks/backup-manager/backup_manager.yml
````

After running it, view backups with:

```bash
ls ~/backups
```

###  Adding More User Folders
Currently this only backs up /Documents.

To back up additional user-level directories (no sudo needed), edit `files_to_backup` in the playbook:

```yaml
files_to_backup:
  - "{{ ansible_env.HOME }}/Documents"
  - "{{ ansible_env.HOME }}/Pictures"
  - "{{ ansible_env.HOME }}/Desktop"
```

###  Adding System / Kernel-Level Folders

To back up system directories like `/etc`, `/var/log`, or `/boot`, enable privilege escalation:

1. Add desired paths:

```yaml
files_to_backup:
  - /etc
  - /var/log
  - /boot
```

2. Run the playbook with sudo:

```bash
ansible-playbook playbooks/backup-manager/backup_manager.yml --ask-become-pass
```

This will allow Ansible to read root-owned directories.


# Output

```bash
angus@angusMintDev:~/Documents/GitHub/ansible-playbooks$ ansible-playbook playbooks/backup-manager/backup_manager.yml

PLAY [Automated Backup Manager (User-Level)] *************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************************************
[WARNING]: Platform linux on host localhost is using the discovered Python interpreter at /usr/bin/python3.12, but future installation of another Python interpreter could change the meaning of that path. See
https://docs.ansible.com/ansible-core/2.16/reference_appendices/interpreter_discovery.html for more information.
ok: [localhost]

TASK [Ensure backup root directory exists] ***************************************************************************************************************************************************************************************
changed: [localhost]

TASK [Create dated backup directory] *********************************************************************************************************************************************************************************************
changed: [localhost]

TASK [Copy files/directories to backup directory] ********************************************************************************************************************************************************************************
changed: [localhost] => (item=/home/angus/Documents)

TASK [Compress backup directory] *************************************************************************************************************************************************************************************************
changed: [localhost]

TASK [Check if compressed backup exists] *****************************************************************************************************************************************************************************************
ok: [localhost]

TASK [Notify success] ************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Backup completed successfully! File: /home/angus/backups/backup-2025-11-18-1710.tar.gz"
}

TASK [Notify failure] ************************************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP ***********************************************************************************************************************************************************************************************************************
localhost                  : ok=7    changed=4    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
angus@angusMintDev:~/Documents/GitHub/ansible-playbooks$ ls ~/backups
2025-11-18-1710  backup-2025-11-18-1710.tar.gz 
```