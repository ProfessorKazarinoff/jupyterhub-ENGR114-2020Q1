# jupyterhub-ENGR114-2020Q1

JupyterHub deployment for Portland Community College's ENGR114 Engineering Programming class Winter 2019

Documentation available at: [https://professorkazarinoff.github.io/jupyterhub-ENGR114-2020Q1/](https://professorkazarinoff.github.io/jupyterhub-ENGR114-2020Q1/)

Attempts to use Ansible playbooks to deploy JupyterHub on Ubuntu 18.04 servers running on Digital Ocean

## Deployment steps

The steps below are still in process:

### Install Ansible on host machine

Install Ansible on host machine (control node). Can be MacOS, Linux Desktop, WSL (Windows Subsystem for Linux) or Linux server.  This machine will run Ansible and the Ansile commands. This machine will not end up with JupyterHub installed on it.

#### On Linux local or remote machine

```text
sudo apt-get update -y update && apt-get -y upgrade
adduser peter #add password
usermod -aG sudo peter
rsync --archive --chown=peter:peter ~/.ssh /home/peter
su - peter
sudo apt install -y ansible
```

#### On MacOS

create a virtual env

```text
conda create -n ansible python=3.7
conda activate ansible
conda istall -c conda-forge ansible
```

### Create SSH keys

On the control node, create an SSH keypair or make sure an exhisting SSH key pair exhists.

#### Create SSH Keys on Linux, WSL

```text
ssh-keygen     # no password, save in default location
```

### Create server

On Digital Ocean create a new server and make sure to add SSH key (and all other SSH keys if using more than one control node)

copy the IP address of the server to the clipboard

### Clone the deployment repo that contains the Ansible playbooks

```text
git clone https://github.com/professorkazarinoff/jupyterhub-ENGR114-2020Q1.git
```

### Create hosts file and add server IP address to it

Create a hosts file that is a copy of the example_hosts file

```text
cd jupyterhub-ENGR114-2020Q1
cp example_hosts hosts
nano hosts
# add IP address to hosts file. ctrl-x to save
```

### Create var.yml file that is copy of example_vars.yml

On the host machine, create a password to use for the managed machine user we are going to create

```text
sudo apt-get install -y whois
mkpasswd --method=sha-512      #copy result to clip board
```

Then on the host machine, add the hashed password, IP addresses, 

```text
cp example_vars.yml vars.yml
nano vars.yml
# add domain name, server IP addresses and hashed password
```

### Run initial server setup playbook

Run the initial server setup playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```<user>``` with your username or use the path to your ```hosts``` file that has the server IP address in it. (still in development: create a password on the control node with the line ```openssl passwd -1 <my text password>``` copy the resulting hashed password into the ```initial_server_setup.yml``` playbook.)

```text
ansible-playbook -i /home/peter/jupyterhub-ENGR114-2020Q1/hosts initial_server_setup.yml
```

### Run miniconda installer playbook

Run the miniconda installer playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```peter``` with your username or use the path to your ```hosts``` file that has the server IP address in it.

```text
ansible-playbook -i /home/peter/jupyterhub-ENGR114-2020Q1/hosts install_miniconda.yml
```

### Run the install jupyterhub playbook

Run the install jupyterhub playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```peter``` with your username or use the path to your ```hosts``` file that has the server IP address in it.

```text
ansible-playbook -i /home/peter/jupyterhub-ENGR114-2020Q1/hosts install_jupyterhub.yml
```

### Link a domain name to DO server

Link a domain name to the Digital Ocean server.

### Run the ssl_cirt playbook

Change the domain name (the one hooked up to Digital Ocean Server) and email address in ```ssl_cirt.yml```. Then run the playbook. This playbook is still in testing phase.

```text
ansible-playbook -i /home/peter/jupyterhub-ENGR114-2020Q1/hosts ssl_cirt.yml
```

### Cookie Secret and Proxy Auth Token

### Install Nginx

### Nginx Config

### Jupyterhub Config

### Jupyterhub as a system service

### Test

### Google OAuth

### Custom Login Page

### Cull Idle Servers script

### Test

## In Development

change vars.yml and hosts then run the site

```text
ansible-playbook -i /home/peter/jupyterhub-ENGR114-2020Q1/hosts site.yml
```
