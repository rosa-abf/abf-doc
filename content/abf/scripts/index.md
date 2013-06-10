---
title: ABF Package build environment
---

# Package build environment

This describes the resources that make up the official Rosa ABF Package build environment. If you have any problems or requests please contact support.

**Note: This Documentation is in a beta state. Breaking changes may occur.**

* [Assembly of packages](/abf/scripts/assembly_of_packages/)
* [Publication of packages](/abf/scripts/publication_of_packages/)

Different scripts uses for each type of platform. If You would like to create new script, we recommend to review next projects:

* [RHEL scripts](https://abf.rosalinux.ru/abf/rhel-scripts)
* [MDV scripts](https://abf.rosalinux.ru/abf/mdv-scripts)

It contains scripts for `MDV` and `RHEL` platforms.

We use [Vagrant](http://docs-v1.vagrantup.com/v1/docs/boxes.html) for manage Virtual Machines. This VMs use for building/publishing packages, creating ISO. You can find boxes which use on ABF:

* [MDV](http://file-store.rosalinux.ru/api/v1/file_stores/60fe76919127188489b997a5c4eb3129dd373081)
* [RHEL](http://file-store.rosalinux.ru/api/v1/file_stores/574ff9ea966bd5d0c521c83029f3b9e2fc94377b)