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
      roles:
        - role: ansible-role_upgrade
          reboot_if_needed: true

License
-------

BSD

Author Information
------------------

    ARK-ICT
    Andre Rikkert de Koe - ICT
