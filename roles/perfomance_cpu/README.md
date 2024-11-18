Perfomance CPU
=========

Enable maximum processor performance

Role Variables
--------------

perfomance_cpu_max_cstate_file_path: /sys/module/intel_idle/parameters/max_cstate - Path to view the current processor operating mode.
perfomance_cpu_max_cstate_value: "1" - Performance value being set.

perfomance_cpu_grub_path: /etc/default/grub.d/ - Path to store grub configuration.
perfomance_cpu_grub_file_name: 50-cloudimg-settings.cfg - Grub configuration file.

perfomance_cpu_reboot_vm_after_apply: false - Perform a reboot after applying the configuration.

Example Playbook
----------------

---
- name: Perfomance CPU
  hosts: all
  become: true
  roles:
    - role: perfomance_cpu
      tags:
        - perfomance_cpu


Examples
-------

### Applying the configuration

```
export ANSIBLE_OPTS="--tags perfomance_cpu"
export ANSIBLE_HOSTS_GROUP="perfomance"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} --become-user=root -b ${ANSIBLE_OPTS} playbooks/perfomance.yaml

```

### Lint testing

```
ansible-lint playbooks/perfomance_cpu.yaml roles/perfomance_cpu
```

### Check mode - simulation
```
export ANSIBLE_OPTS="--tags perfomance_cpu"
export ANSIBLE_HOSTS_GROUP="perfomance"
export ANSIBLE_INVENTORY_FILE="hosts"s"

eval ansible-playbook --check --diff -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} -b ${ANSIBLE_OPTS} playbooks/perfomance.yaml
```
