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

# Launch EC2 with python
#! /bin/bash
yum install python-pip -y

# INSTALLATION: (So better go with apt - So skip this and go to next block)
sudo pip install ansible 
sudo yum install ansible
sudo apt install ansible

By apt/yum --> Inventory & Config files are created by default
    * inventory files --> /etc/ansible/hosts
    * config files --> /etc/ansible/ansible.cfg
By PIP --> inventory & config files to be created manually
    * inventory files --> vi slaves.txt (add all slave node private ip's one by one in new line)
    * config files --> download from the github official (wget https://gist.githubusercontent.com/alivx/2a4ca3e577ead4bd38d247c258e6513b/raw/fe2b9b1c7abc2b52cc6998525718c9a40c7e02a5/ansible.cfg)

# INSTALLATION USING APT:
apt update
apt install -y ansible
which python
which ansible

* /etc/ansible/ansible.cfg :- It is a configuration file here we are going to tell how ansible should be running.
* /etc/ansible/hosts:- whatever machines that we want ansible to connect that information we are going to give in this file. It is the default file and we can change it later, it is called an inventory file.
* Goto /etc/ansible/ansible.cfg, here everything is commented so uncomment “inventory” and “sudo-user”.
* vi /etc/ansible/hosts ---> you can give slave machine which you want to connect ip, username, keyfile path
* ansible -m ping all

(-i slaves.txt can be ignored if installed via apt/yum)

# ADHOC COMMANDS --> run single task
* ansible all -i slaves.txt -m ping
    -i --> referring the file where slave node IP's are present to connect to them
    -m --> modules

* ansible all -i slaves.txt  -a "uptime"
    -a --> actions

# STATES
- install = present
- uninstall = absent
- start = started
- stop = stopped
- restart = restarted
- become ---> sudo/root user

## EXAMPLE:
yum install httpd -y
service httpd start

* ansible all -i slaves.txt -m yum -a "name=httpd state=present" -b
* ansible all -i slaves.txt -m service -a "name=httpd state=started" -b
* ansible all -i slaves.txt -m copy -a "src=/home/ec2-user/index.html dest=/var/www/html/index/html" -b

# PLAYBOOK:
ansible-playbook -i slaves.txt basic.yml