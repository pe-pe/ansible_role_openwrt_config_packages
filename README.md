OpenWRT Config Packages
=========

[![CI](https://github.com/pe-pe/ansible_role_openwrt_config_packages/workflows/CI/badge.svg)](https://github.com/pe-pe/ansible_role_openwrt_config_packages/actions)

Ansible role that installs packages on OpenWRT device.

Requirements
------------
None

Role variables
--------------
Packages to be installed on OpenWRT device are defined in `openwrt_config_packages` variable.
```yaml
openwrt_config_packages:
  - diffutils
  - bash
```
If `openwrt_config_packages` configuration variable is not present - no changes are made by role.

Dependencies
------------
This role depends on Ansible role `gekmihesg.openwrt` which allows to manage OpenWRT and derivatives with Ansible but without Python.

Example playbook using the role
-------------------------------
`./host_vars` \
`./host_vars/myrouter.yml`
```yaml
---
openwrt_config_packages:
  - diffutils
  - bash
```
`./inventory.ini`
```ini
[openwrt]
myrouter
```
`./roles` \
`./roles/requirements.yml`
```yaml
---
roles:
- name: gekmihesg.openwrt
- name: pe_pe.openwrt_config_packages
```
`./site.yml`
```yaml
---
- hosts: all
  roles:
    - role: gekmihesg.openwrt
    - role: pe_pe.openwrt_config_packages
```
`./ansible.cfg`
```ini
[defaults]
# Define inventory location
inventory = ./inventory.ini
# Where to put roles downloaded from galaxy and other repos
roles_path = ./roles
# Defaults to /tmp to avoid flash wear on target device
remote_tmp = /tmp
```

Example execution
-----------------
Install roles and requirements:
```
ansible-galaxy role install -r roles/requirements.yml
```
Preview changes execution would perform on inventory:
```
ansible-playbook site.yml --check --diff
```
Execute playbook on inventory:
```
ansible-playbook site.yml
```
License
-------
MIT

Author Information
------------------
PePe
