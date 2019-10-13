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

### Create server

### Run initial playbook

### Run conda install playbook

### Run SSL playbook

