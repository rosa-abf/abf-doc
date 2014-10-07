---
title: Deployment with Ansible | ABF Worker Deployment Documentation
---

# Deployment with [Ansible](http://www.ansible.com)

* [Prepare environment](#prepare-environment)
* [Deploy](#deploy)

## Prepare environment

Install __Ansible__ on local PC, see: [http://docs.ansible.com/intro_installation.html](http://docs.ansible.com/intro_installation.html)

## Deploy

You should have access by **ssh** as **root** user for all servers.
All command should be called from local PC.

    git clone git@abf.io:abf/abf-ansible.git
    cd abf-ansible
    cp abf-worker.hosts.example abf-worker.hosts
    # Update "abf-worker.hosts" file
    # NOTE: for MDV distros you should run this command more 2 times as minimum
    ansible-playbook -i abf-worker.hosts abf-worker.yml
