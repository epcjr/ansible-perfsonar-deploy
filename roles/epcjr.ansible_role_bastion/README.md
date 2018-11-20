bastion
=========

This bastion role sets up secure communications to a bastion host.

Requirements
------------

* Ansible on the jumpbox / bastion host
* bastion role installed

      $ ansible-galaxy install -f epcjr.bastion

Role Variables
--------------

Group Variables, and their default values:

      
      # This is a list of bastion users with ssh keys.  They will be
      # provisioned with user accounts on the target nodes, and
      # their ssh keys will be copied over.
      #
      bastion_users: []
      
      # This is the default group for the list of bastion users.
      #
      bastion_user_group: nobody
      
      # This is a list of bastion jumpboxes.
      # ssh will be restricted on the target nodes to these machines
      # only.
      #
      bastion_jumpboxes: []
            
      # A list of nameservers to add to resolv.conf
      #
      bastion_nameservers: []

Host Variables, only set on a per-host basis.  They are undeclared by default.

      # Set the hostname of the machine if set
      #
      bastion_hostname:
      
Dependencies
------------

None.

Example Playbook
----------------

bastion_site.yml:

    - hosts: all
      vars_files:
        - vars/bastion_vars.yml
      roles:
         - { role: epcjr.bastion }

vars/bastion_vars.yml:

      # General perfsonar node settings
      bastion_users:
        - myuid
      bastion_user_group: staff
      bastion_hosts:
        - bastion.example.com
      bastion_nameservers:
        - 8.8.8.8
        - 8.8.4.4
        - 2001:4860:4860::8888
        - 2001:4860:4860::8844

host_vars/example_ps_host

      # Set target hostname
      bastion_hostname: example_target_host


License
-------

Apache 2.0
