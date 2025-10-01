# VM Provisioner Role

An Ansible role to create and manage KVM virtual machines using libvirt.

## Requirements

- libvirt and KVM installed on the target host
- `community.libvirt` collection installed
- Appropriate permissions to manage libvirt (user in libvirt group)

## Role Variables

See `defaults/main.yml` for all available variables with defaults.

## Example Playbook

### Create a single VM:
```yaml
- hosts: hypervisor
  roles:
    - role: vm-provisioner
      vars:
        vm_name: "my-vm"
        vm_memory: 2048
        vm_vcpus: 2
        vm_iso_path: "/path/to/ubuntu.iso"
        
# VM-creation-KVM-linux

- check resources of the lab (not part of the playbook)
- create a role for VM creation
- customize it with variables file
- test it 


# structure 
vm-playbooks/
├── inventories/
│   └── hosts.ini
├── playbooks/
│   └── create_vms.yml
├── roles/
│   └── vm_creation/
│       ├── tasks/
│       │   ├── check_resources.yml
│       │   └── main.yml
│       ├── vars/
│       │   └── main.yml
│       └── templates/
│           └── vm.xml.j2
└── vars/
    └── vm_specs.yml


#after creation of VMs
- set a fixed IP for the machine
- set a hostname 
- test ip + hostname
- test machines can communicate with each other ping


# How to run playbook
ansible-galaxy collection install community.libvirt #on host                                                                   
ansible 127.0.0.1 -m ping                                                                      
ansible-playbook playbooks/playbook-createvm.yml -v --ask-become-pass                                                                              



# Tests done
- test playbook when the a VM with same name exist                                                                
- test VM creation 
- test OS installation automatically using cloud-init image
- test setting hostname 
- test setting user + password 