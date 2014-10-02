---
title: ABF Deployment Documentation
---

# ABF Deployment Documentation

This describes the resources that make up the official Rosa ABF Deployment Documentation. If you have any problems or requests please contact support.

**Note: This Documentation is in a beta state. Breaking changes may occur.**

* [Prepare environment](#prepare-environment)
* [Deploy](#deploy)

## Prepare environment

You should have access by **ssh** as **root** user for all servers.
All command should be called from local PC

    # Install "ansible", see: http://docs.ansible.com/intro_installation.html
    git clone git@abf.io:abf/abf-ansible.git
    cd abf-ansible

## Deploy

    cp rosa-build.hosts.example rosa-build.hosts
    # Update "rosa-build.hosts" and "rosa-build.yml" files
    ansible-playbook -i rosa-build.hosts rosa-build.yml