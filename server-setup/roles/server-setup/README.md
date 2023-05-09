# Server Setup

This role configures servers to my liking.

## Requirements

* An Ansible playbook and inventory file and configures which hosts will be configured.
* Some paths or environment variables with the paths to critical files.
  * Inventory
  * Roles
  * Vault (has been refactored that this can be ignored.)

## Example Execution

```bash
cd /path/to/playbook
export ANSIBLE_INVENTORY=$(realpath "$PWD"/inventories)
export ANSIBLE_CONFIG=$(realpath /path/to/your/ansible/config)
export ANSIBLE_ROLES_PATH=$(realpath "$PWD"/roles)
export ANSIBLE_VAULT_PASSWORD_FILE=/path/to/your/ansible/vault
```
* This assumes you have set `ANSIBLE_ROLES_PATH` and `$ANSIBLE_INVENTORY` set.
* `-k` is needed for your `ssh` password since passwordless `ssh` isn't configured yet.

```bash
# Accept the server fingerprint 1 at a time :(
# Could accept all without checking but this has security implications.
ansible -i $ANSIBLE_INVENTORY all -m ping -k --forks=1 

# Run the play to configure servers.
ansible-playbook -i $ANSIBLE_INVENTORY playbook.yml -k
```
