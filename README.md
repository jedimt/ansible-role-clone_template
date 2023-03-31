Ansible Role: Clone Template VM
=========

Clones a template VM from a backup NFS mount to local VCSA.

Requirements
------------

A valid VMware virtual machine template hosted on a NFS share.

Role Variables
--------------

The following vars are defined in vars/main.yml

    # Vault credentials
    vcenter_username: "{{ vault_vcenter_username }}"
    vcenter_password: "{{ vault_vcenter_password }}"

The following vars are defined in defaults/main.yml

    # vCenter variables
    vcenter_datacenter: "SC0"
    vcenter_cluster: "AppFactory"
    vcenter_hostname: "devvcsa.tme.nebulon.com"

    # Folder to register the VM into
    vcenter_vm_folder: "Kubernetes"

    # Details on NFS mount holding backup of the VM template
    nfs_backup_name: backup
    vm_backup_template_name: "ubuntu20.04.4"

Dependencies
------------

None.

Example Playbook
----------------

    # ===========================================================================
    # Clone template VM to VCSA
    # ===========================================================================
    - name: Clone template VM to VCSA
    hosts: localhost
    connection: local
    gather_facts: false
    become: false
    module_defaults:
        group/vmware:
        hostname: '{{ vcenter_hostname }}'
        username: '{{ vcenter_username }}'
        password: '{{ vcenter_password }}'
        validate_certs: false
    tags: play_clone_template

    vars_files:
        # Ansible vault with all required passwords
        - "../../credentials.yml"

    roles:
        - ansible-role-clone-template


License
-------

MIT

Author Information
------------------

Aaron Patten
aaronpatten@gmail.com
