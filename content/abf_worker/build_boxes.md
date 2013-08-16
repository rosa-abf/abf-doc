---
title: Build boxes | ABF Worker Documentation
---

# Build boxes

* [Install OS](#install-os)
* [Prepare environment](#prepare-environment)
* [Build box](#build-box)

We use [Vagrant](http://docs-v1.vagrantup.com/v1/docs/boxes.html) for manage Virtual Machines on [VirtualBox](https://www.virtualbox.org/). This VMs use for building/publishing packages, creating ISO. You can find boxes which uses on [ABF](https://abf.rosalinux.ru/abf/abf-worker/blob/master/config/vm.yml.sample)

For each arches (`i586`, `x86_64`, ...) we use single box by default. But you can create own box for each arches.

## Install OS

`HDD` of `VM` should has the next specification:

* `ext4` not less 50Gb
* `swap` not less 35GB (will be use for `tmpfs`)
* format of `HDD` should be `VDI`

Password for `root` user should be `vagrant`.

## Prepare environment

### First of all we should add new user.

Add new user `vagrant` with password `vagrant`:

    useradd vagrant && passwd vagrant

Add admin rights for user `vagrant` (update `/etc/sudoers` file):

* add `%vagrant ALL=(ALL) NOPASSWD: ALL` line 
* remove `Defaults requiretty` line

Set `PermitRootLogin without-password` in `/etc/ssh/sshd_config` file.

### Configure ssh access for `vagrant` user

    mkdir -p /home/vagrant/.ssh
    cd /home/vagrant/.ssh
    curl -L -O https://raw.github.com/warpc/vagrant/master/keys/vagrant.pub
    mv vagrant.pub authorized_keys && chmod 600 authorized_keys
    chmod 600 /home/rosa/.ssh/authorized_keys
    chmod 700 /home/rosa/.ssh
    chown -R vagrant:vagrant /home/vagrant

### Install VirtualBox Guest Additions

[Full instruction](http://www.virtualbox.org/manual/ch04.html#idp19235216)

Download [VBoxGuestAdditions 4.2.6](http://download.virtualbox.org/virtualbox/4.2.6/VBoxGuestAdditions_4.2.6.iso) on the main `PC` and attach `iso` to `VM`.

On `VM`:

    sudo mkdir /media/cdrom0
    sudo mount -t iso9660 /dev/cdrom /media/cdrom0/
    cd /media/cdrom0/
    sudo ./VBoxLinuxAdditions.run
    # Install extra packages if something go wrong and try again
    # sudo ./VBoxLinuxAdditions.run
    cd ~ && sudo umount /dev/cdrom && sudo rm -rf /media/cdrom0/

### Install nesessary packages

    mock openssh-client openssh-server git-core ruby

Add `vagrant` user into 'mock' group

    usermod -a -G mock vagrant

## Build box

We use custom version of `vagrant`. For package `VM` into box you should configure [abf-worker](https://abf.rosalinux.ru/abf/abf-worker) project (install `rvm`, `ruby`, `gems`).

Then you will be able to create box:

    vagrant package --base '<name of VM>’ --output '<name of box>.box'

