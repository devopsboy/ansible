### ANSIBLE:
- Configuration management tool
- PUSH mechanism (control node --> managed nodes)
- https://docs.ansible.com

# PREREQUISITES:
Control Node:
- python
- ansible
Managed Node:
- python

# INSTALLATION:
sudo apt update
sudo apt install python3
sudo apt install -y ansible
which python
which ansible

* /etc/ansible/ansible.cfg :- It is a configuration file here we are going to tell how ansible should be running.
* /etc/ansible/hosts:- whatever machines that we want ansible to connect that information we are going to give in this file. It is the default file and we can change it later, it is called an inventory file.
* ansible -m ping all

* /etc/ansible/ansible.cfg:
==========================
[defaults]
inventory = /etc/ansible/hosts

* /etc/ansible/hosts:
====================
[ec2-instances]
ec2-instance-1 ansible_host:<IP> ansible_user:ubuntu ansible_ssh_private_key_file:<PEM FILE PATH>
ec2-instance-2 ansible_host:<IP> ansible_user:ubuntu ansible_ssh_private_key_file:<PEM FILE PATH>

# ADHOC COMMANDS --> run single task
* ansible all -m ping
    -i --> referring the file where slave node IP's are present to connect to them
    -m --> modules

* ansible all -a "uptime"
    -a --> actions

# STATES
- install = present
- uninstall = absent
- start = started
- stop = stopped
- restart = restarted
- become ---> sudo/root user

## EXAMPLE:
apt install nginx -y

* ansible all -m yum -a "name=httpd state=present" -b
* ansible all -m copy -a "src=/home/ubuntu/index.html dest=/var/www/html/index.html" -b

# PLAYBOOK:
ansible-playbook file.yml