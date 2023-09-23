Realtek Fix
=========
This is the ansible role to fix the realtek driver issue on proxmox. This role will install the realtek driver version 8168 instead of the 8169 driver on the proxmox host and will fix the issue of realtek causing intermittent issues.

Specifically, this role will do the following:
- Update repositories to include non-free and non-free-updates ( if set to proxmox_subscription: false ) otherwise you will need to sort the repositories yourself
- Install pve-headers
- Install the realtek driver 8168
- Blacklist the 8169 driver
- Update grub parameters for the realtek driver
- Reboot the proxmox host

Requirements
------------
This role was tested on proxmox 8.0 but should work on any proxmox version as it is not a proxmox specific role. 

Role Variables
--------------
The only variable we set is `proxmox_subscription: false` which will update the repositories to include non-free and non-free-updates. If you have a proxmox subscription, you can set this to true and it will not update the repositories.

Dependencies
------------
none

Example Playbook
----------------
```yaml
- name: realtek.yml
  hosts: proxmox
  gather_facts: true
  vars_prompt: 
  - name: "ansible_password"
    prompt: "Enter the remote password"
    private: yes
  vars: 
    ansible_user: root
  tasks:
  - import_role:
      name: realtek-fix
```
