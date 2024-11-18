Rename Interfaces
=========

The role of interface renaming. For Ubuntu OS.

Role Variables
--------------

rename_interfaces_interface_name_from: xxx0 - Name of the interface to be renamed
rename_interfaces_interface_name_to: xxx0 - New interface name

rename_interfaces_netplan_config_file_src: 70-configuration-ansible.conf.j2 - Configuration template name
rename_interfaces_netplan_config_file_dst: /etc/netplan/configuration-ansible.conf - Saved configuration file
rename_interfaces_netplan_config_file_mode: "0600" - Saved file mode

Example Playbook
----------------

---
- name: Rename Interfaces
  hosts: all
  become: true
  roles:
    - role: rename_interfaces
      tags:
        - rename_interfaces


Examlpes
-------

### Applying the configuration

```
export ANSIBLE_OPTS='--tags rename_interfaces'
export ANSIBLE_HOSTS_GROUP="rename_interfaces"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} --become-user=root -b ${ANSIBLE_OPTS} playbooks/rename_interfaces.yaml
```

### Lint testing

```
ansible-lint playbooks/rename_interfaces.yaml roles/rename_interfaces
```

### Check mode - simulation
```
export ANSIBLE_OPTS='--tags rename_interfaces'
export ANSIBLE_HOSTS_GROUP="rename_interfaces"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook --check --diff -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} -b ${ANSIBLE_OPTS} playbooks/rename_interfaces.yaml
```
