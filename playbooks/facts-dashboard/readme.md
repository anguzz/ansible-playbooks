# System dashboard

To run this dashboard run


- Install apache  `sudo apt install apache2 -y`
- Ensure ansible is installed and run `ansible-playbook playbooks/facts-dashboard/facts_dashboard.yml --ask-become-pass`
- view at `http://localhost:80/facts.html` the default port used for apache.



## Troubleshooting errors

If you enter your sudo password wrong Gathering facts will hang up. Interupt the process and re-try.

```bash
angus@angusMintDev:~/Documents/GitHub/ansible-playbooks$ ansible-playbook playbooks/facts-dashboard/facts_dashboard.yml --ask-become-pass
BECOME password: 

PLAY [Generate system facts HTML dashboard] **************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************************************************************

^C [ERROR]: User interrupted execution****************************************************************************************************************************************************************************************************
```
