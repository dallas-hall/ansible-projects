# Server Setup

This role configures servers to my liking.

## Requirements

* An Ansible playbook and inventory file and configures which hosts will be configured.
* Some paths or environment variables with the paths to critical files.
  * Inventory
  * Roles
  * Vault

```bash
cd /path/to/playbook
export ANSIBLE_INVENTORY=$(realpath /path/to/inventory)
export ANSIBLE_CONFIG=$(realpath /path/to/your/ansible/config)
export ANSIBLE_ROLES_PATH=$(realpath /path/to/this/role)
export ANSIBLE_VAULT_PASSWORD_FILE=/path/to/your/ansible/vault

```

## Example Playbook

```yaml
---
- name: Configure servers to my liking.
  hosts:
    - all
  become: no
  gather_facts: yes
  #strategy: debug
  roles:
    - server-setup

```

## Examples Inventory

```yaml
all:
  hosts:
    jumpbox[1:2].example.com:
    devbox[1:2].example.com:
    qabox[1:2].example.com:
    staging[1:2].example.com:
    spark-cluster[1:5].example.com:
    k8s-cluster[1:5].example.com:
    app-vm[1:5].example.com:
  vars:
    ansible_user: dhall
    ansible_connection: ssh
```

# Example Execution
```bash
ansible-playbook -i $ANSIBLE_INVENTORY playbook.yml -k
```
* This assumes you have set `ANSIBLE_ROLES_PATH` and `$ANSIBLE_INVENTORY`
* `-k` probably is needed for your `ssh` password
