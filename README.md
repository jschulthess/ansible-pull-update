# ansible-pull-update
Update your system via ansible-pull

## Introduction

This repository contains playbooks to update a Linux system using ansible-pull. It is intended as a simple yet reasonably useful example of running Ansible in _pull_ mode.

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

The ansible-pull command can be run in one of two ways:

1. manually
2. unattended

### Manual Usage 

To run the *ansible-pull* manually use a command like the following:

```
url='https://github.com/jschulthess/ansible-pull-update.git' # URL of the playbook repository
checkout='develop'                                            # branch/tag/commit to checkout
directory='/var/projects/ansible-pull-update'           # directory to checkout repository to
logfile='/var/log/ansible-pull-update.log'                            # where to put the logs

sudo ansible-pull -o -C ${checkout} -d ${directory} -i ${directory}/inventory -U ${url} \
  2>&1 | sudo tee -a ${logfile}
```

### Unattended Usage

To make the playbook run unattended at regular intervals the above command is typically installed as a cron job.
For convenience a playbook "ansible-pull-setup.yml" has been included which can be used to install the cron job and log rotation.

Note: before running the playbook to install make sure to set the reposigory URL by replacing the string SUPPLY_YOUR_OWN_GIT_URL_HERE in the playbook.

To install, simply run the playbook on the host to be ansible-pull enabled.

```
ansible-playbook ansible-pull-setup.yml
```

The playbook creates a cron entry which runs _ansible-pull_ every 15 minutes. Check the logfine and verify that an attempt to update the system is indeed done regularly.

### Integration

The roles subdirectory contains a role "provision_ansible_pull_update" which can be used to integrate the ansible-pull execution into a provisioning system like ['Foreman/Katello'](https://theforeman.org/).  
This allows to apply ansible-pull as a simple role on any host in Foreman using the ['foreman_ansible'](https://github.com/theforeman/foreman_ansible) plugin.  

The role contains the following variables that can be overridden:

  * schedule: Cron schedule. Default: ```'*/15 * * * *'```  

  * cron_user: User to run ansible-pull as from cron. Default: "root"  

  * logfile: File that ansible will use for logs. Default: /var/log/ansible-pull.log  

  * workdir: Directory to where repository will be cloned. Default: /var/lib/ansible/local  

  * repo_url: Repository to check out -- YOU MUST CHANGE THIS  
              The repo must contain a local.yml file at top level  

