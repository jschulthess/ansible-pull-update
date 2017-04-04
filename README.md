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
ansible-pull -o -C develop -d /var/projects/ansible-pull-update -i /var/projects/ansible-pull-update/inventory -U git://github.com/jschulthess/ansible-pull-update >> /var/log/ansible-pull-update.log 2>&1
```
