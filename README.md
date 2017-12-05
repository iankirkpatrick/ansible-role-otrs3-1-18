otrs3.1.18
==========

This role will install all necessary dependencies for otrs3.1.18, download otrs3.1.18, unpack and apply the base configuration. Once complete the otrs configuration can be completed at:<br><br>

https://<hostname>/otrs/installer.pl

Dependencies
------------

This role assumes that you are logging on with a user account and using sudo to run commands with root privileges. For this to be successful, the following should be defined in your hosts/inventory file:

[otrs-servers]
otrs-host1

[otrs-servers:vars]
ansible_connection=ssh
ansible_user=<user>
ansible_ssh_pass=<userpass>
ansible_become_pass=<userpass>
mysql_root_pass=<mysql-root-password>

It is recommended that you use ansible-vault encrypt <inventory-file> to encrypt the file as it includes sensitive user account information. The script can then be run with the "--ask-vault-pass" option to prompt for the vault key before executing. The mysql root password is defined in the inventory file to prevent mysql being installed without a password for root access. This password will be required later when running through the installer for otrs.
It goes without saying that the user defined in the inventory file must have sudo permissions to allow the tasks under this role to complete successfully.

Example Playbook
----------------

This role can be used in a playbook as follows: 

---
- name: Install and configure otrs server
  hosts: otrs-servers
  become: yes
  become_method: sudo
  roles:
    - { role: iankirkpatrick.otrs3.1.18 }

License
-------

MIT
