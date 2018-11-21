# Ansible role for install Zabbix-Agent on the Windows Server


### Tested platforms are:
* Windows Server 2012 R2


### Version available:
* 3.4.6 (i386, amd64)
* 4.0.0 (i386, amd64)


### Dependency:
This role uses the WinRM module on the local and remote machine.
WinRM module for local machine:
```
pip install https://github.com/diyan/pywinrm/archive/master.zip#egg=pywinrm
```


WinRM module for Windows machine (use PowerShell console):
```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://github.com/ansible/ansible/raw/devel/examples/scripts/ConfigureRemotingForAnsible.ps1'))"
```


### Role Variables:
* zabbix_agent_version - variable for pick version (3 for 3.4.6 / 4 for 4.0.0)
* zabbix_agent_version_hw - optional variable for change hw zabbix agent version (i386 or 32 for i386 / amd64 or 64 use amd64)
* zabbix_agent_url_v3 - variable for setting URL of zabbix-agent archive (Version 3.4.6 i386 and amd64)
* zabbix_agent_url_v4_i386 - variable for setting URL of zabbix-agent archive (Version 4.0.0 i386)
* zabbix_agent_url_v4_amd64 - variable for setting URL of zabbix-agent archive (Version 4.0.0 amd64)
* zabbix_server_ip - variable for setting IP address of zabbix-server
* zabbix_server_active_ip - variable for setting IP address of zabbix-server active
* zabbix_agent_ip - listen IP address in zabbix-agent configuration
* zabbix_agent_port - listen port in zabbix-agent configuration
* zabbix_agent_timeout - timeout for working query in zabbix-agent 
* zabbix_agent_remote_cmd - variable for set EnableRemoteCommands (remote commands from zabbix server)



### Example inventory file:
```
[windows]
10.10.10.4

[windows:vars]
ansible_ssh_user=Administrator
ansible_ssh_port=5986
ansible_connection=winrm
ansible_winrm_server_cert_validation=ignore
```


### Example playbook task (Version 3.4.6 i386):
```
---
- hosts: windows
  remote_user: Administrator
  vars:
    - zabbix_server_ip: '10.10.10.22'
    - zabbix_server_active_ip: '127.0.0.1'
    - zabbix_agent_version: '3'
    - zabbix_agent_version_hw: 'i386'
  roles:
    - { role: qwsj.win-zabbix-agent }
```


### Example playbook task (Version 4.0.0 amd64):
```
---
- hosts: windows
  remote_user: Administrator
  vars:
    - zabbix_server_ip: '10.10.10.22'
    - zabbix_server_active_ip: '127.0.0.1'
    - zabbix_agent_version: '4'
    - zabbix_agent_version_hw: 'amd64'
  roles:
    - { role: qwsj.win-zabbix-agent }
```


Have issue? [https://github.com/qwsj/win-zabbix-agent/issues](https://github.com/qwsj/win-zabbix-agent/issues)

Ansible user guide for Windows: [https://docs.ansible.com/ansible/latest/user_guide/windows.html](https://docs.ansible.com/ansible/latest/user_guide/windows.html)

Ansible Galaxy: [https://galaxy.ansible.com/qwsj/win-zabbix-agent/](https://galaxy.ansible.com/qwsj/win-zabbix-agent/)
