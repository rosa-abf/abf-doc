---
title: Deployment on Ubuntu | ABF Deployment Documentation
---

# Deployment on Ubuntu

* [Prepare environment](#prepare-environment)
* [Prepare server to deployment](#prepare-server-to-deployment)
* [Startup ABF](#startup-abf)

## Prepare environment

### First of all we should add new users.

Add new users `rosa`, `git` and add necessary groups:

    sudo useradd rosa && sudo passwd rosa
    sudo useradd git && sudo usermod -a -G rosa git && sudo usermod -a -G git rosa

Add admin rights for user `rosa` (update `/etc/sudoers` file):

  * add `%rosa ALL=(ALL) NOPASSWD: ALL` line 
  * remove `Defaults requiretty` line

### Install nesessary packages

    sudo apt-get update && sudo apt-get install curl git patch postgresql postfix imagemagick autoconf automake libtool nginx libicu-dev postgresql-server-dev-9.1 ruby1.9.1

### Install RVM (for `git` and `rosa` users):

To install RVM type in this command:

    curl -L get.rvm.io | bash -s stable

After it is done installing, load RVM.

    source ~/.rvm/scripts/rvm

In order to work, RVM has some of its own dependancies that need to be installed.

    rvm requirements

### Install Ruby (for `git` and `rosa` users):

Once you are using RVM, installing Ruby is easy.

    rvm install ruby-2.1.3

Ruby is now installed. However, since we accessed it through a program that has a variety of Ruby versions, we need to tell the system to use 2.1.3 by default.

    rvm use ruby-2.1.3 --default

### Install RubyGems (for `git` and `rosa` users):

The next step makes sure that we have all the required components of Ruby on Rails. We can continue to use RVM to install gems; type this line into terminal.

    rvm rubygems current

### Install PostgreSQL

See solution by installation: [Install PostgreSQL](http://www.if-not-true-then-false.com/2012/install-postgresql-on-fedora-centos-red-hat-rhel)

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

    wget http://redis.googlecode.com/files/redis-2.6.10.tar.gz
    tar zxvf redis-2.6.10.tar.gz
    cd redis-2.6.10 && make && sudo make install
    sudo mkdir /etc/redis && sudo cp redis.conf /etc/redis

    cd ~ && wget https://abf.rosalinux.ru/abf/abf-configs/raw/master/ubuntu/redis.conf
    sudo mv redis-server /etc/init.d/redis-server && sudo chmod +x /etc/init.d/redis-server
    sudo useradd redis && sudo touch /var/log/redis.log && sudo chown redis:redis /var/log/redis.log
    sudo mkdir -p /var/lib/redis && sudo chown redis:redis /var/lib/redis

    sudo update-rc.d redis-server defaults

Startup Redis server:

    sudo /etc/init.d/redis-server start


### Configure postfix

Solution for fix: `OpenSSL::SSL::SSLError: hostname does not match the server certificate`

Update `/etc/postfix/main.cf` file:

    sudo nano /etc/postfix/main.cf 

from:

    smtpd_use_tls = yes
    smtpd_tls_cert_file = /etc/pki/tls/certs/postfix.pem
    smtpd_tls_key_file = /etc/pki/tls/private/postfix.pem

to

    smtpd_use_tls = no
    #smtpd_tls_cert_file = /etc/pki/tls/certs/postfix.pem
    #smtpd_tls_key_file = /etc/pki/tls/private/postfix.pem

Then restart postfix:

    sudo service postfix restart

### Configure Nginx

If You have SSL certificates which not `self signed` You can add their for nginx:

    /etc/ssl/abf.key
    /etc/ssl/abf.crt 

Solution for creating `self signed` SSL Certificate on nginx: [How to Create a SSL Certificate](https://www.digitalocean.com/community/articles/how-to-create-a-ssl-certificate-on-nginx-for-centos-6). But no warranty for correct working of all system.

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
