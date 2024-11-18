Crypto Disk
=========

Encrypting disks, mounting, unmounting and closing an encrypted disk.


Role Variables
--------------

crypto_disk_unmount_all: false - Unmounting, closing the disk. Recommended to specify in the console when starting the playbook.

crypto_disk_crypto_passphrase: changeme - Disk encryption password. It is better to use the value from vault (crypto_disk_crypto_passphrase: "{{ lookup('community.hashi_vault.hashi_vault', passphrasse:value) }}").

crypto_disk_partitioning_parted_list: - List of disks to enable encryption.
  - crypto_luks_device_name: cryptoDisk
    crypto_luks_device_device: /dev/xxx
    crypto_luks_device_state: present
    crypto_luks_device_state_opened: opened
    parted_device: /dev/xxx
    parted_partEnd: 100%
    parted_number: 1
    parted_label: msdos
    parted_removeDevice: false
    parted_newPartition: true
    parted_part_start: 0%
    filesystem_fstype: ext4
    filesystem_opts: -cc
    mount_path: /mnt
    mount_fstype: ext4
    mount_state: absent

Example Playbook
----------------

---
- name: Perfomance CPU
  hosts: all
  become: true
  roles:
    - role: crypto_disk
      tags:
        - crypto_disk

Examples
-------

### Disk encryption and mounting

```
export ANSIBLE_OPTS='--tags crypto_disk'
export ANSIBLE_HOSTS_GROUP="cryptodisk"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} --become-user=root -b ${ANSIBLE_OPTS} playbooks/crypto_disk.yaml
```

### Unmounting the disk and closing it

```
export ANSIBLE_OPTS='--tags crypto_disk --extra-vars {\"crypto_disk_unmount_all\":true}'
export ANSIBLE_HOSTS_GROUP="cryptodisk"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} --become-user=root -b ${ANSIBLE_OPTS} playbooks/crypto_disk.yaml
```


### Lint testing

```
ansible-lint playbooks/crypto_disk.yaml roles/crypto_disk
```

### Check mode - simulation.
```
export ANSIBLE_OPTS='--tags crypto_disk'
export ANSIBLE_HOSTS_GROUP="cryptodisk"
export ANSIBLE_INVENTORY_FILE="hosts"

eval ansible-playbook --check --diff -i ${ANSIBLE_INVENTORY_FILE} -l ${ANSIBLE_HOSTS_GROUP} -b ${ANSIBLE_OPTS} playbooks/crypto_disk.yaml
```
