# Why Ansible ??
Ansible uses push machanism over chef, pupet tools
#
Ansible is agentless

# Prerequests:
===========

1) Launch EC2 Instance on AWS - Ubuntu 22.04LTS ( For Ansible Server )
2) Launch EC2 Instance on AWS - Ubuntu 22.04LTS ( Target machine for Ansible ) - 2 No.s Machines
   update ubuntu server
   $ sudo apt-get update

# create directory for ansible server
$ mkdir ansible

# Change Directory to ansible 
$ cd ansible

# Install Ansible on ubuntu 22.04LTS (Ansible Server )
$ sudo apt-get install ansible

# Proceducer to make password less access between ansible server & target servers (Hosts)

# On the Ansible Server 
$ssh-keygen

Generating public/private rsa key pair.
Enter file in which to save the key (/home/ubuntu/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ubuntu/.ssh/id_rsa
Your public key has been saved in /home/ubuntu/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:QXqPwOGaYfBvy7LOuw+iTagIb8HBWFuox7PUcbnk1jQ ubuntu@ip-172-31-52-120
The key's randomart image is:
+---[RSA 3072]----+
|  ..  ...        |
|  oooo++E        |
| * ++==+o.       |
|o O..=+o.+       |
| + +o.o S .      |
| .+  o .         |
|o o.o o          |
|+=.o +           |
|+.o.*+.          |
+----[SHA256]-----+

# list .ssh file
$ ls /home/ubuntu/.ssh/
authorized_keys  id_rsa  id_rsa.pub

# copy content from id_rsa.pub
$ cat ~/.ssh/id_rsa.pub

OR
# ~/ansible$ cat /home/ubuntu/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDpmQmmezsLfIp5bdl+Ml2Jp2CDGxrfIa/xqR0xuFHUk8k8DRxZt27MkIYDFuRz1nOAXiDyrGguzb5y674Vk6UhywZ+NdlLvtLu7rp0ivO/bN80geyCsgGy1FVCD77a0bZw5j9mQCan
T8YJiE6a9a53dF7D87XommNCvhYKsXaE1DyIGgUOgMtDh8TE591gWcbguQ9sIKF0J1KcxDv4sdypGJu1RY2KC97epk2wGZQDVV60R3HbMcqspQx1KRdabHtA7h2gjI9swaAAm9WFhQ1aIOO91iXaRcLqIcIhGg9/OmGequ9TB2ljB1C1
x6WUrHsg6cMYQwfMj/hpgKM4mYBJGQxC6osj7ZfRKb7gK7pu65en1Ws0krowYcUqtVH3dKapr2sl0iZDdAXshiuO8ciYdenQ4Wg/6QJry6bJm6ALzv2e/2wzey8DAD8oivppInh/BVC6QUnb4/mveYuaXEtlUTG9NXsPLr35xlzCSYnz
20y2YoFiPF2t1PWYSD/3jts= ubuntu@ip-172-31-52-120

# Paste to target server's
$ vim ~/.ssh/authorized_keys 

Verify Password less access to target servers from ansible servers
ssh < private Ip of vm's >

# On the Ansible server
# Create Inventory file and servers by groups 
$ vim inventory 
[webserver]
172.31.41.443
172.56.59.118

[dbservers]
172.56.89.107
172.58.98.112

# Ansible Ad-Hoc Commands 
$ ansible -i inventory 172.31.41.443 -m "shell" -a "touch devops" 

# For all inventory 
$ ansible -i inventory all -m "shell" -a "touch devops" 

# For webservers
$ ansible -i inventory webservers -m "shell" -a "touch devops" 

# Ansible Playbook commands
$ ansible-playbook inventory <playbook_name>

# Ansible Galaxy Commands ( Ansible Roles )
$ ansible-galaxy kubernates 



