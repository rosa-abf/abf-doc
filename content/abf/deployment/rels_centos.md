---
title: RosaLab ABF Documentation - Deployment on RELS/CentOS
---

# RosaLab ABF Documentation - Deployment on RELS/CentOS

* <a href="#prepare-environment">Prepare environment</a>
* <a href="#prepare-server-to-deployment">Prepare server to deployment</a>
* <a href="#startup-abf">Startup ABF</a>

## Prepare environment

### First of all we should add new users.

Add new users `rosa`, `git` and add necessary groups:

    sudo useradd rosa && sudo passwd rosa
    sudo useradd git && sudo usermod -a -G rosa git && sudo usermod -a -G git rosa

Add admin rights for user `rosa` (update `/etc/sudoers` file):

  * add `%rosa ALL=(ALL) NOPASSWD: ALL` line 
  * remove `Defaults requiretty` line

### Install nesessary packages

    sudo yum install -y git-core libicu-devel gcc ruby-devel libxml2 libxml2-devel libxslt libxslt-devel postgresql-devel nginx postfix python-devel crontabs openssl

### Install RVM (for `git` and `rosa` users):

To install RVM type in this command:

    curl -L get.rvm.io | bash -s stable

After it is done installing, load RVM.

    source ~/.rvm/scripts/rvm

In order to work, RVM has some of its own dependancies that need to be installed. You can see what these are:

    rvm requirements

In the text that RVM shows you, look for this paragraph.
Additional Dependencies:

    For Ruby / Ruby HEAD (MRI, Rubinius, & REE), install the following:
    ruby: yum install -y gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison iconv-devel

Go ahead and download the recommended dependancies, being careful not to use sudo. Instead, we should use rvmsudo:

    rvmsudo yum install -y gcc-c++ patch readline readline-devel zlib zlib-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison iconv-devel

### Install Ruby (for `git` and `rosa` users):

Once you are using RVM, installing Ruby is easy.

    rvm install ruby-1.9.3-p392 

Ruby is now installed. However, since we accessed it through a program that has a variety of Ruby versions, we need to tell the system to use 1.9.3 by default.

    rvm use ruby-1.9.3-p392 --default

### Install RubyGems (for `git` and `rosa` users):

The next step makes sure that we have all the required components of Ruby on Rails. We can continue to use RVM to install gems; type this line into terminal.

    rvm rubygems current

### Install PostgreSQL

See solution by installation: <a href="http://www.if-not-true-then-false.com/2012/install-postgresql-on-fedora-centos-red-hat-rhel">Install PostgreSQL</a>

The next step updates `.bashrc` file:

    PATH=/usr/pgsql-9.2/bin:$PATH

## Prepare server to deployment

### Create folders for web:

    sudo mkdir /srv && sudo chown -R rosa:rosa /srv && mkdir -p /srv/rosa_build/shared/tmp

### Start services on Boot

    sudo chkconfig --levels 2345 nginx on
    sudo chkconfig crond on
    sudo service crond start

### Configure ssh access for `git` and `rosa` users

    sudo mkdir -p /home/{rosa,git}/.ssh && sudo touch /home/{rosa,git}/.ssh/authorized_keys &&
    sudo chmod 600 /home/{rosa,git}/.ssh/authorized_keys &&
    sudo chown -R rosa:rosa /home/rosa && sudo chown -R git:git /home/git

Add Your public key into `~rosa/.ssh/authorized_keys`

### Configure PostgreSQL

Change to `postgres` user

    sudo su postgres

Create new user

    createuser -D -P -E -e rosa
    Enter password for new role: rosa
    Enter it again: rosa
    Shall the new role be a superuser? (y/n) n
    Shall the new role be allowed to create more new roles? (y/n) n

Create database

    createdb -O rosa -e rosa_build

### Configure Git

From `rosa` user

    git config --global user.name Rosa
    git config --global user.email rosa@abf.rosalinux.ru

Solution for showing filenames with Cyrillic alphabet

    git config --global core.quotepath false

### Configure Redis DB

See solution by installation: <a href="https://abf.rosalinux.ru/abf/abf-configs/blob/master/rhel/redis_install.sh">Install Redis DB</a>

    wget https://abf.rosalinux.ru/abf/abf-configs/raw/master/rhel/redis_install.sh
    chmod +x redis_install.sh
    sudo ./redis_install.sh

### Configure Nginx

If You have SSL certificates which not `self signed` You can add their for nginx:

    /etc/ssl/abf.key
    /etc/ssl/abf.crt 

Solution for creating `self signed` SSL Certificate on nginx: <a href="https://www.digitalocean.com/community/articles/how-to-create-a-ssl-certificate-on-nginx-for-centos-6">How to Create a SSL Certificate</a>. But no warranty for correct working of all system.

Configuration files for nginx:

    cd /etc/nginx/
    sudo curl -L -O https://abf.rosalinux.ru/abf/abf-configs/raw/master/nginx/nginx.conf
    cd /etc/nginx/conf.d/

without SSL certificates:

    sudo curl -L -O https://abf.rosalinux.ru/abf/abf-configs/raw/master/nginx/rosa_build.http.conf
    sudo mv rosa_build.http.conf rosa_build.conf

with SSL certificates:

    sudo curl -L -O https://abf.rosalinux.ru/abf/abf-configs/raw/master/nginx/rosa_build.https.conf
    sudo mv rosa_build.https.conf rosa_build.conf

Then restart nginx:

    sudo service nginx restart

### Configure iptables

Update `/etc/sysconfig/iptables` file:

  * add `-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT` line 
  * add `-A INPUT -m state --state NEW -m tcp -p tcp --dport 443 -j ACCEPT` line (if has SSL certificates)
  * remove `-A FORWARD -j REJECT --reject-with icmp-host-prohibited` line

Then restart iptables:
    
    sudo service iptables restart

### Configure ssh access for git

    sudo su - git
    env GIT_SSL_NO_VERIFY=true git clone https://abf.rosalinux.ru/abf/gitlab-shell.git
    cp gitlab-shell/config.yml.example gitlab-shell/config.yml

Update `config.yml` as You like:

    # GitLab user. git by default
    user: git

    # Url to gitlab instance. Used for api calls
    # Use http instead of https when no ssl certificates
    gitlab_url: "https://127.0.0.1/"

    # Repositories path (APP_CONFIG[‘git_path’] + ‘/git_projects’)
    repos_path: "/home/rosa/gitstore/git_projects"

### Archivation of Logs

    sudo vi /etc/logrotate.d/redis

    /var/log/redis_*.log {
       weekly
       rotate 10
       copytruncate
       delaycompress
       compress
       notifempty
       missingok
    }

    sudo vi /etc/logrotate.d/rosa_build

    /srv/rosa_build/shared/log/*.log {
      weekly
      missingok
      rotate 52
      compress
      delaycompress
      notifempty
      copytruncate
    }

## Startup ABF

On DEV machine:

    cap production deploy:setup
    cap production deploy:check
    cap production deploy:update

On server:

    cd /srv/rosa_build/current && RAILS_ENV=production bundle exec rake db:seed

Update all configuration files:

    /srv/rosa_build/shared/config/application.yml
    /srv/rosa_build/shared/config/newrelic.yml

Startup:

    cap production deploy:start
