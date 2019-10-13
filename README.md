# jupyterhub-ENGR114-2020Q1

JupyterHub deployment for Portland Community College's ENGR114 Engineering Programming class Winter 2019

Uses Ansible playbooks to deploy JupyterHub on Ubuntu 18.04 servers running on Digital Ocean

## Deployment steps

The steps below are still in process:

### Install Ansible on host machine

Install Ansible on host machine (control node). Can be MacOS, Linux Desktop, WSL (Windows Subsystem for Linux) or Linux server.  This machine will run Ansible and the Ansile commands. This machine will not end up with JupyterHub installed on it.

#### On Linux local or remote machine

```
sudo apt update
sudo apt upgrade
sudo apt install ansible
```

#### On MacOS

create a virtual env

```
conda create -n ansible python=3.7
conda activate ansible
conda istall -c conda-forge ansible
```

### Create SSH keys

On the control node, create an SSH keypair or make sure an exhisting SSH key pair exhists.

#### Create SSH Keys on Linux, WSL

```
ssh-keygen
```

### Create server

On Digital Ocean create a new server and make sure to add SSH key (and all other SSH keys if using more than one control node)

copy the IP address of the server to the clipboard

### Clone the deployment repo that contains the Ansible playbooks

```
git clone https://github.com/professorkazarinoff/jupyterhub-ENGR114-2020Q1.git
```

### Create hosts file and add server IP address to it

Create a hosts file that is a copy of the example_hosts file

```
cd jupyterhub-ENGR114-2020Q1
cp example_hosts hosts
nano hosts
# add IP address to hosts file. ctrl-x to save
```

### Run initial server setup playbook

Run the initial server setup playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```<user>``` with your username or use the path to your ```hosts``` file that has the server IP address in it.

```
ansible-playbook -i /home/<user>/jupyterhub-ENGR114-2020Q1/hosts initial_server_setup.yml
```

### Run miniconda installer playbook

Run the miniconda installer playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```<user>``` with your username or use the path to your ```hosts``` file that has the server IP address in it.

```
ansible-playbook -i /home/<user>/jupyterhub-ENGR114-2020Q1/hosts install_miniconda.yml
```

### Run the install jupyterhub playbook

Run the install jupyterhub playbook using ```ansible-playbook```. Supply the hosts file as inventory. Make sure the ```(ansible)``` virtual environment is active first. Make sure to replace ```<user>``` with your username or use the path to your ```hosts``` file that has the server IP address in it.

```
ansible-playbook -i /home/<user>/jupyterhub-ENGR114-2020Q1/hosts install_jupyterhub.yml
```

### Link a domain name to DO server

Link a domain name to the Digital Ocean server.

### Run the ssl_cirt playbook

Change the domain name (the one hooked up to Digital Ocean Server) and email address in ```ssl_cirt.yml```. Then run the playbook. This playbook is still in testing phase.

```
ansible-playbook -i /home/<user>/jupyterhub-ENGR114-2020Q1/hosts ssl_cirt.yml
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
