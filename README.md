# netology_ansible_1

1. Значение 12.

2. Это файл group_vars/examp.yml

3. Заменил:

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook/group_vars/all$ cat examp.yml
---
  some_fact: all default fact

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook/group_vars/all$ 
```

4. 

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ sudo docker ps -a
CONTAINER ID        IMAGE                      COMMAND             CREATED             STATUS              PORTS               NAMES
dcc88d847b15        pycontribs/centos:7        "sleep 600000"      3 seconds ago       Up 2 seconds                            centos7
6349766c526d        pycontribs/ubuntu:latest   "sleep 600000"      2 minutes ago       Up 2 minutes                            ubuntu
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ sudo ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] *****************************************************************************************************************************************************

TASK [Gathering Facts] ****************************************************************************************************************************************************
[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible
releases. A future Ansible release will default to using the discovered platform python for this host. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version 2.12. Deprecation
warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] ***********************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] *********************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el"
}
ok: [ubuntu] => {
    "msg": "deb"
}

PLAY RECAP ****************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$
```

5-6.

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ sudo ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ***********************************************************************************************************************************************************************

TASK [Gathering Facts] **********************************************************************************************************************************************************************
[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible releases. A future
Ansible release will default to using the discovered platform python for this host. See https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more
information. This feature will be removed in version 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] *****************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ***************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP **********************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$
```

7-8.

Запустилось только с явной опцией --ask-vault-pass:

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ sudo ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password:

PLAY [Print os facts] *********************************************************************************************************************************

TASK [Gathering Facts] ********************************************************************************************************************************
[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility
with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host. See
https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for more information. This feature will be removed in version
2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] ***************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] *************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ********************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$
```

9. 

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ ansible-doc -l | grep apt
apt                                                           Manages apt-packages
apt_key                                                       Add or remove an apt key
apt_repo                                                      Manage APT repositories via apt-repo
apt_repository                                                Add and remove APT repositories
apt_rpm                                                       apt_rpm package manager
fortios_switch_controller_security_policy_captive_portal      Names of VLANs that use captive portal authentication in Fortinet's FortiOS and Fort...
na_ontap_qos_adaptive_policy_group                            NetApp ONTAP Adaptive Quality of Service policy group
na_ontap_ucadapter                                            NetApp ONTAP UC adapter configuration
nios_naptr_record                                             Configure Infoblox NIOS NAPTR records
skydive_capture                                               Module which manages flow capture on interfaces
vmware_guest_network                                          Manage network adapters of specified virtual machine in given vCenter infrastructure
vmware_vmkernel                                               Manages a VMware VMkernel Adapter of an ESXi host
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playboome@me-HP-260-G3-DM:
```

10. 

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/netology_ansible_1/playbook/inventory$ cat prod.yml 
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker

  inside:
    hosts:
      localhost:
        ansible_connection: local

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/netology_ansible_1/playbook/inventory$ 
```

11.

```
me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$ sudo ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
[sudo] password for me:
Vault password:

PLAY [Print os facts] ******************************************************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************************************************
[DEPRECATION WARNING]: Distribution Ubuntu 20.04 on host localhost should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible releases. A
future Ansible release will default to using the discovered platform python for this host. See https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for
 more information. This feature will be removed in version 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [localhost]
[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible releases. A
future Ansible release will default to using the discovered platform python for this host. See https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html for
 more information. This feature will be removed in version 2.12. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] ************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] **********************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "all default fact"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP *****************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

me@me-HP-260-G3-DM:~/netology/DZ_Ansible_1/playbook$
```










