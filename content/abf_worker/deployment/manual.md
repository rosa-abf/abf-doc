---
title: ABF Worker Deployment | ABF Worker Documentation
---

# ABF Worker Deployment Documentation

* [Prepare environment](#prepare-environment)
* [Startup ABF Worker](#startup-abf-worker)

## Prepare environment

### First of all we should add new user.

Add new user `rosa`:

    sudo useradd rosa

Add admin rights for user `rosa` (update `/etc/sudoers` file):

  * add `%rosa ALL=(ALL) NOPASSWD: ALL` line 
  * remove `Defaults requiretty` line

Set `PermitRootLogin without-password` in `/etc/ssh/sshd_config` file.

### Create TMP folder:

    sudo mkdir -p /mnt/store/tmp/abf-worker-tmp && sudo chown rosa:rosa -R /mnt/store/tmp

### Install nesessary packages

    git-core procmail zlib-devel


### Install RVM (for `rosa` user):

To install RVM type in this command:

    curl -L get.rvm.io | bash -s stable

After it is done installing, load RVM.

    source ~/.rvm/scripts/rvm

In order to work, RVM has some of its own dependancies that need to be installed.

    rvm requirements

### Install Ruby (for `rosa` user):

Once you are using RVM, installing Ruby is easy.

    rvm install ruby-2.1.1

Ruby is now installed. However, since we accessed it through a program that has a variety of Ruby versions, we need to tell the system to use 2.1.1 by default.

    rvm use ruby-2.1.1 --default

### Install RubyGems (for `rosa` user):

The next step makes sure that we have all the required components of Ruby on Rails. We can continue to use RVM to install gems; type this line into terminal.

    rvm rubygems current

## Startup ABF Worker

On DEV machine:

    cap production deploy:setup
    cap production deploy:check
    cap production deploy:update

Update all configuration files in `/home/rosa/abf-worker/shared/config`:

    resque.yml
    application.yml
    newrelic.yml
    vm.yml

Startup:

    cap production deploy:update
    cap deploy:rpm
