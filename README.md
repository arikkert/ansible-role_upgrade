upgrade
=========

Update the OS and packages
- RedHat family: **dnf update -y**
- Debian family: **apt update; apt full-upgrade**

Optionally reboot the target host if needed

Requirements
------------

- RedHat family: *yum-utils* should be installed or in repo
- Debian family: *needrestart* should be installed or in repo

Target host should be upgradeable so have working repositories configured

Role Variables
--------------

*reboot_if_needed*: boolean (default false)

When true the target host will be rebooted after upgrade when needed

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      become: true # upgrade/reboot need root perms
      serial: 1 # if servers should be upgraded/rebooted one by one
      roles:
        - role: ansible-role_upgrade
          reboot_if_needed: true

      # Optional extra checks before continuing
      # e.g. when upgrading all nodes in k8s cluster one by one
      tasks:
        - name: Wait for all nodes to be ready
          become_user: "{{ k8s_user }}"
          ansible.builtin.command: kubectl get nodes
          register: result
          until:
            - result.rc == 0
            - '"NotReady" not in result.stdout'
          changed_when: false
          check_mode: false

License
-------

BSD

Author Information
------------------

    ARK-ICT
    Andre Rikkert de Koe - ICT
