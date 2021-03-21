# rh134env
This is a RHCE study environment built with Vagrant

### Requirements
The following tools are required to be install on the host:

- Vagrant 2.2.9

- Version 6.1.18 r142142 (Qt5.14.2)

### rh134env architecture
![architecture](https://github.com/midu16/rh134env/blob/main/doc/lab-design.png)


- The VMs after the spawn-up without any customization.

- The user should perform the following tasks manually:
```
	- create the username ansible with redhat password on all the hosts.

        - generate the ssh-key from the controller.example.com and share it with the node{1..}.example.com

        - [vagrant@controller ~]$ sudo yum install ansible
         
        - [vagrant@controller ~]$ ansible --version
		ansible 2.9.18
  		config file = /home/vagrant/ansible.cfg
  		configured module search path = ['/home/vagrant/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  		ansible python module location = /usr/lib/python3.8/site-packages/ansible
  		executable location = /usr/bin/ansible
  		python version = 3.8.2 (default, Feb 28 2020, 00:00:00) [GCC 10.0.1 20200216 (Red Hat 10.0.1-0.8)]
```

### Basic ansible configuration
The project is providing a basic ```ansible.cfg``` and ```inventory```, the transfer would be possible as in the following example:
```
$ scp controller.example.com.ansible/* vagrant@10.10.10.200:/home/vagrant
vagrant@10.10.10.200's password: 
ansible.cfg                                                                                                             100%  176   475.8KB/s   00:00    
inventory                                                                                                               100%  351     1.5MB/s   00:00    
```

### Testing the environment for the first time

After all the manual configurations, lets give a spin of ```ansible``` and test the environment functionality.

```
[vagrant@controller ~]$ ansible all -m ping

DEPRECATION WARNING]: Distribution fedora 32 on host node3.example.com should use /usr/bin/python3, but is using /usr/bin/python for backward 
compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
node3.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
[DEPRECATION WARNING]: Distribution fedora 32 on host node4.example.com should use /usr/bin/python3, but is using /usr/bin/python for backward 
compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
node4.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
[DEPRECATION WARNING]: Distribution fedora 32 on host node1.example.com should use /usr/bin/python3, but is using /usr/bin/python for backward 
compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
node1.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
[DEPRECATION WARNING]: Distribution fedora 32 on host node2.example.com should use /usr/bin/python3, but is using /usr/bin/python for backward 
compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
node2.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
[DEPRECATION WARNING]: Distribution fedora 32 on host controller.example.com should use /usr/bin/python3, but is using /usr/bin/python for backward 
compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See 
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. 
Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
controller.example.com | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

