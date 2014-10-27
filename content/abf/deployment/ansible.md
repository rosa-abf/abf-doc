---
title: Deployment with Ansible | ABF Deployment Documentation
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
    cp rosa-build.hosts.example rosa-build.hosts
    # Update "rosa-build.hosts" and "rosa-build.yml" files
    # Put your ssh public key into a roles/user/files/ssh-keys folder
    ansible-playbook -i rosa-build.hosts rosa-build.yml