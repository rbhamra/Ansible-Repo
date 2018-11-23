# How to Use

From the roles directory of your project folder clone in to this repository.

```
rupesh@master oracle # git clone https://github.com/rbhamra/Ansible-Role.git

```

Once the repository is cloned, you're almost good to go. Most of the default vaules are functional, and they're listed under the defaults/main.yml.

There are two parameters which need to be customized to suite your environment.

1. oracle_installer_path 

This is the path to the installer archives, that's downloaded from Oracle.

2. oracle_images

This is a array of all the available oracle images listed. Based on the version specified in the array, the correct image will be picked for installation.

```
oracle_images:
    - { image: "{{ oracle_installer_path }}/linux.x64_11gR2_database_1of2.zip", version: "11.2.0.1" }
    - { image: "{{ oracle_installer_path }}/linux.x64_11gR2_database_2of2.zip", version: "11.2.0.1" } 
    - { image: "{{ oracle_installer_path }}/linuxx64_12201_database.zip", version: "12.2.0.1" }
```

# Ansible Playbook

For a typical installation you can follow the following Syntax. 

The following playbook can be used to install Oracle 11gR2 instance with SID "demo",  
```
---

- name: install oracle
  hosts: "{{ host_group }}"
  become: yes
  become_method: sudo
  roles:
    - oracle_install
  vars:
    oracle_edition: EE
    oracle_version: 11.2.0.1
    install_mode: INSTALL_DB_AND_CONFIG
    oracle_db_name: demo
```

However, if the requirement is to install only the software binaries and not to create the database....

NOTE: We're specifying oracle 12c in the case, but oracle 11g would work the same way.

```
---

- name: install oracle
  hosts: "{{ host_group }}"
  become: yes
  become_method: sudo
  roles:
    - oracle_install
  vars:
    oracle_edition: EE
    oracle_version: 12.2.0.1
    install_mode: INSTALL_DB_SWONLY
```


# Pre-requisites for the playbook
This playbook will install the oracle 12c software package only
