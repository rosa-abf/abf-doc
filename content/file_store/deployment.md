---
title: File Store Deployment | File Store Documentation
---

# Deployment

* [Prepare environment](#prepare-environment)
* [Deploy](#deploy)

## Prepare environment

You should have access by **ssh** as **root** user for all servers.
All command should be called from local PC

    # Install "ansible", see: http://docs.ansible.com/intro_installation.html
    git clone git@abf.io:abf/abf-ansible.git
    cd abf-ansible

## Deploy

    cp file-store.hosts.example file-store.hosts
    # Update "file-store.hosts" file
    ansible-playbook -i file-store.hosts file-store.yml
