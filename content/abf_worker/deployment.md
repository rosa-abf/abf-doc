---
title: ABF Worker Deployment | ABF Worker Documentation
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

    cp abf-worker.hosts.example abf-worker.hosts
    # Update "abf-worker.hosts" file

    # NOTE: for MDV distros you should run this command more 2 times as minimum
    ansible-playbook -i abf-worker.hosts abf-worker.yml

