# Molecule Vagrant demo

This demo shows how to use Molecule to test an Ansible role on multiple OSes at the same time using Vagrant.

The role is located in ansible/roles/system and was created with:

``` bash
ansible-galaxy init system
```

The molecule scenario was created in ansible/roles/system with:

``` bash
molecule init scenario --driver-name vagrant
```

## Usage

Create the VM that will have nested VMs create by Molecule:

``` bash
cd vagrant
vagrant up
```

Enter the VM to start molecule:

``` bash
vagrant ssh
cd /vagrant/ansible/roles/system
```

Create the Molecule VMs:

``` bash
molecule create
```

Install the role:

``` bash
molecule converge
```

Run the tests:

``` bash
molecule verify
```

Destroy the VMs:

``` bash
molecule destroy
```

To run everything in one go:

``` bash
molecule test
```

To run everything in one go but leave the VMs alive:

``` bash
molecule test --destroy never
```

To ssh into one of the VMs, first retrieve its ID using

``` bash
vagrant global-status
id       name       provider   state   directory                                    
------------------------------------------------------------------------------------
a77ef7e  centos7    virtualbox running /home/vagrant/.cache/molecule/system/default 
a88f4e2  almalinux8 virtualbox running /home/vagrant/.cache/molecule/system/default
```

and then use the ID to ssh into the VM:

``` bash
vagrant ssh a77ef7e
```

## Known issues

For some reason Vagrant on the host looses its metadata after molecule creates the Vagrant VMs in the VM.
No idea why yet.
