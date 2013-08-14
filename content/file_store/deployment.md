---
title: File Store Deployment | File Store Documentation
---

# Deployment

* [Prepare environment](#prepare-environment)
* [Prepare server to deployment](#prepare-server-to-deployment)
* [Startup File Store](#startup-file-store)

## Prepare environment

### First of all we should add new user.

Add new user `rosa`:

    sudo useradd rosa


### Install nesessary packages

    git-core libicu-devel gcc ruby-devel libxml2 libxml2-devel libxslt libxslt-devel postgresql-devel python-devel

### Install RVM (for `rosa` user):

To install RVM type in this command:

    curl -L get.rvm.io | bash -s stable

After it is done installing, load RVM.

    source ~/.rvm/scripts/rvm

In order to work, RVM has some of its own dependancies that need to be installed. You can see what these are:

    rvm requirements

In the text that RVM shows you, look for paragraph “Additional Dependencies”:

    sudo apt-get update && sudo apt-get --no-install-recommends install bash curl git patch bzip2 build-essential openssl libreadline6 libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev libgdbm-dev ncurses-dev automake libtool bison subversion pkg-config libffi-dev

    rvm --skip-autoreconf pkg install iconv


### Install Ruby (for `rosa` user):

Once you are using RVM, installing Ruby is easy.

    rvm install ruby-2.0.0-p247

Ruby is now installed. However, since we accessed it through a program that has a variety of Ruby versions, we need to tell the system to use 2.0.0 by default.

    rvm use ruby-2.0.0-p247 --default

### Install RubyGems (for `rosa` user):

The next step makes sure that we have all the required components of Ruby on Rails. We can continue to use RVM to install gems; type this line into terminal.

    rvm rubygems current

### Install PostgreSQL

See solution by installation: [Install PostgreSQL](http://www.if-not-true-then-false.com/2012/install-postgresql-on-fedora-centos-red-hat-rhel)

The next step updates `.bashrc` file:

    PATH=/usr/pgsql-9.2/bin:$PATH

## Prepare server to deployment

### Create folders for web:

    sudo mkdir -p /srv/rosa_file_store/shared/tmp && sudo chown -R rosa:rosa /srv

### Configure ssh access for `rosa` user

    sudo mkdir -p /home/rosa/.ssh && sudo touch /home/rosa/.ssh/authorized_keys &&
    sudo chmod 600 /home/rosa/.ssh/authorized_keys &&
    sudo chown -R rosa:rosa /home/rosa

Add Your public key into `/home/rosa/.ssh/authorized_keys`

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

    createdb -O rosa -e rosa_file_store

### Configure Nginx

    mkdir /home/rosa/nginx
    sudo -i
    wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.31.tar.gz
    tar -xf pcre-8.31.tar.gz
    cd /home/rosa/nginx/pcre-8.31
    ./configure
    make && make install

    cd ..
    wget http://nginx.org/download/nginx-1.3.8.tar.gz
    tar -xf nginx-1.3.8.tar.gz

    wget https://github.com/downloads/masterzen/nginx-upload-progress-module/nginx_uploadprogress_module-0.9.0.tar.gz
    wget http://www.grid.net.ru/nginx/download/nginx_upload_module-2.2.0.tar.gz

    tar -xf nginx_uploadprogress_module-0.9.0.tar.gz
    tar -xf nginx_upload_module-2.2.0.tar.gz

    cd /home/rosa/nginx/nginx-1.3.8
    ./configure --prefix=/usr/share/nginx \
    --sbin-path=/usr/sbin/nginx \
    --conf-path=/etc/nginx/nginx.conf \
    --error-log-path=/var/log/nginx/error.log \
    --http-log-path=/var/log/nginx/access.log \
    --with-http_flv_module \
    --with-http_ssl_module \
    --with-http_gzip_static_module \
    --add-module=/home/rosa/nginx/modules/upload \
    --add-module=/home/rosa/nginx/modules/upload-progress \
    make && make install

    ## fix nginx: error while loading shared libraries:
    ## libpcre.so.1: cannot open shared object file: No such file or directory
    ln -s /usr/local/lib/libpcre.so.1 /lib64 

Start `nginx` on Boot:

    sudo chkconfig --levels 2345 nginx on
    service nginx stop
    service nginx start


### Configure iptables

Update `/etc/sysconfig/iptables` file:

  * add `-A INPUT -m state --state NEW -m tcp -p tcp --dport 80 -j ACCEPT` line 

Then restart iptables:
    
    sudo service iptables restart


## Startup File-Store

On DEV machine:

    cap production deploy:setup
    cap production deploy:check
    cap production deploy:update

On server:

    cd /srv/rosa_file_store/current && RAILS_ENV=production bundle exec rake db:seed

Update all configuration files:

    /srv/rosa_file_store/shared/config/application.yml
    /srv/rosa_file_store/shared/config/newrelic.yml

Startup:

    cap production deploy:start