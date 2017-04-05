# ansible-pull-update
Update your system via ansible-pull

## Introduction

This repository contains playbooks to update a Linux system using ansible-pull.

At present it supports the following OS variants:

- RHEL 7+, Centos 7+
- Fedora
- Ubuntu (>16.04)

## Prerequisite

Ansible needs to be installed in order to run any Ansible playbook.

On most Linux distributions installing Ansible is a simple package install:

On Ubuntu do:
```
sudo apt install ansible
```

On Fedora do:
```
sudo dnf install -y ansible
```

Similarly, on RHEL/CentOS do:
```
sudo yum -y install ansible
```

Or refer to the official [installation documentation](http://docs.ansible.com/ansible/intro_installation.html)

## Usage

```
url='git@github.com:jschulthess/ansible-pull-update.git' # URL of the playbook repository
checkout='develop'                                        # branch/tag/commit to checkout
directory='/var/projects/ansible-pull-update'       # directory to checkout repository to
logfile='/var/log/ansible-pull-update.log'                        # where to put the logs

sudo ansible-pull -o -C ${checkout} -d ${directory} -i ${directory}/inventory -U ${url} \
  2>&1 | sudo tee -a ${logfile}
```
