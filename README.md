# ansible-role-install-ansible-venv

CentOS7 / RHEL7 - Install Ansible for different versions of Ansible inside "virtual environments" (using python-virtualenv) on localhost (Ansible control server).  

This tasks can also remove old versions. Just make sure you aren't using the virtual environment you have configured to be removed.  

To use: Type `ansible-activate` and use tab completion to pick the specific version.  
To stop using venv, type: `deactivate`  

NOTE: You need ansible installed first for this to work.  
Also, after running the playbook, logout and log in again to enable the bash completion aliases.

Available versions can be found here:  
<https://pypi.org/project/ansible/> from <https://github.com/ansible/ansible/releases>  

## Group Variables

./group_vars/centos-dev/proxy.yml  
With a proxy:

```yaml
proxy_env:
  http_proxy: http://my.internal.proxy:80
  https_proxy: https://my.internal.proxy:80
```

With no proxy:

```yaml
proxy_env: []
```

## Default Settings

```yaml
#Ansible control server is behind a proxy
install_ansiblev_proxy_enabled: true
install_ansiblev_virtualenv_basepath: /opt/virtualenvs
install_ansiblev_versions_add:
  - "2.3.3"
  - "2.4.6"
  - "2.5.15"
  - "2.6.18"
  - "2.7.12"
  - "2.8.2"
install_ansiblev_versions_remove:
  - "2.6.5"
  - "2.7"
```

## Example Playbook install-ansible-venv.yml

```yaml
---
- hosts: '{{inventory}}'
  become: yes
  roles:
  - install-ansible-venv
```

## Usage

Install Ansible into virtual environments:

```bash
ansible-playbook install-ansible-venv.yml --extra-vars "inventory=localhost" -i hosts-dev
```

After running the playbook, logout and log in again to enable the bash completion aliases.
