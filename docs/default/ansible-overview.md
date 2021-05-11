# ansible

## concepts

- Ansible runs agentless. The remote machine just needs ssh installed (and for many modules python and pip).
- the machine which got the executables installed is called **control node**
- the managed machines are called **managed nodes** or informally **hosts**
- a list of managed nodes is called **inventory** or informally **hostfile**
- **modules** are the units of code Ansible executes 
- a **task** executes a module with very specific arguments
- a **playbook** is a executable list of ansible task

*playbook and play will often get used synonymously. A playbook is the yaml file which may container one or more plays. A play is seperated by --- in the yaml file)*

## up and running

### install

- [official guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-debian)
- (optional) For an ansible Web-UI you may want to take a look at Ansible Tower respective it open source version [AWX](https://github.com/ansible/awx) 

#### control node:

Add the following line to **/etc/apt/sources.list**:

deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
sudo apt update
sudo apt install ansible
```

#### managed node

- open ssh port
- python installed (for most modules)
- pip installed (for most modules)


**Remember that the managed nodes need to have ssh activated and python and pip installed.**

### create inventory

[Official guide](https://docs.ansible.com/ansible/latest/user_guide/intro_inventory.html)

You can add managed nodes in the file **/etc/ansible/hosts** either via the ini format or via the yaml format. Or set path via the`-i` flag. Hostfiles need to have the following rights: `sudo chmod 744 /etc/ansible/hosts` and might otherwise clain that the file cannot be parsed ("Unable to parse /etc/ansible/hosts as an inventory source").

A simple host file in ini format:

```ini
192.168.0.2 ansible_user=pi
```

A simple host file in yaml format:

```yaml
all:
  hosts:
    name_of_node:
      ansible_host: 192.168.0.2
      ansible_user: pi
```

Add your public ssh key to the managed nodes ~/.ssh/known_hosts files. Use the `ssh-copy-id` command or copy it manually. Use `ansible all -m ping` to test if all nodes in your inventory are reachable. 


## ad-hoc commands

[official guide](https://docs.ansible.com/ansible/latest/user_guide/intro_adhoc.html#intro-adhoc)

The syntax of a ad-hoc command is as following:

```shell
# ansible [pattern] -m [module] -a "[module options]"

# use of ping module
ansible all -m ping

# a exmaple which is run on all hosts 
ansible all -a "/bin/echo hello"
```

If you do not specify otherwise the ad-hoc will be run by the command module.

## playbooks

[official guide](https://docs.ansible.com/ansible/latest/user_guide/playbooks.html#working-with-playbooks)

- playbooks are defined in yaml format
- To run a playbook: `ansible-playbook playbook_file.yml`
- prerequisite for most modules like docker_image or docker_container: **the host has python and pip installed**

To run a playbook on one host you can:

1. define the host explicitly in the playbook instead of using the all target
2. define the host field as a external variable (`{{target}}`) and set it via command line (`ansible-playbook playbook.yml --extra-vars "target=pi"`)
3. run the playbook with a given a specific host file which contains only the one client (`ansible-playbook -i host-pi.yml playbook.yml`)

install software via playbook:

```yml
---
- hosts: name_of_node
  tasks:
    - name: Install Java
      package: name='java-1.8.0-openjdk' state=latest
```

*This example uses the [package](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/package_module.html) module with no arguments.*

start docker container via playbook:

```yml
---
- hosts: all
  become: true
  vars:
    container_name: hello-world
    container_image: hypriot/armhf-hello-world
  tasks:
  
  - name: install docker module for python
    pip:
      name: docker

  - name: pull docker image
    docker_image:
      name: "{{ container_image }}"
      source: pull

  - name: start docker containers
    docker_container:
      name: "{{ container_name }}"
      image: "{{ container_image }}"
      state: present
```
*This example uses the [pip](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/pip_module.html), [docker_image](https://docs.ansible.com/ansible/latest/collections/community/general/docker_image_module.html) and the [docker_container](https://docs.ansible.com/ansible/latest/collections/community/general/docker_container_module.html) module with a set of arguments.*

**Note: there was an error while using dokcer_image module [No module named ssl_match_hostname](https://github.com/docker/docker-py/issues/1502). The solution was to run `sudo apt-get remove python-configparser`**

## optional grouping of managed nodes

You can address the all nodes in a group via `ansible optional_group_name -m ping` and a specific node by its name `ansible name_of_node -m ping`

A host file witch uses groups (children) and a node without a group in yaml format:

```yaml
all:
  hosts:
    name_of_node_without_group:
      ansible_host: 192.168.0.2
      ansible_user: pi
  children:
    group_name1:
      hosts:
        name_of_node_g1_1:
          ansible_host: 192.168.0.3
          ansible_user: pi
        name_of_node_g1_2:
          ansible_host: 192.168.0.4
          ansible_user: pi
      group_name2:
        hosts:
          name_of_node_g2_1:
            ansible_host: 192.168.0.5
            ansible_user: pi
```
