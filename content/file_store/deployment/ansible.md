---
title: Deployment with Ansible | File Store Deployment Documentation
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
    cp file-store.hosts.example file-store.hosts
    # Update "file-store.hosts" file
    ansible-playbook -i file-store.hosts file-store.yml
