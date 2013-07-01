---
title: Publication of packages | ABF Package build environment
---

# Publication of packages

* [Introduction](#introduction)
* [build.sh script](#buildsh-script)
* [rollback.sh script](#rollbacksh-script)
* [resign.sh script](#resignsh-script)
* [Return codes](#return-codes)

## Introduction

Different scripts uses for each type of platform. If You would like to create new script, we recommend to review next projects:

* [RHEL scripts](https://abf.rosalinux.ru/abf/rhel-scripts/tree/master/publish-packages)
* [MDV scripts](https://abf.rosalinux.ru/abf/mdv-scripts/tree/master/publish-packages)

It contains scripts for `MDV` and `RHEL` platforms.

### Three scripts uses for working with repository:

  * `build.sh`
  * `resign.sh`
  * `rollback.sh`

## build.sh script

`build.sh` uses for publishing packages into repository, regenerating metadata and creating container.
Information about container see:
[Create container](/abf/api/v1/build_lists/#create-container)


### Input parameters:

* `RELEASED` - realise status of platform;
* `REPOSITORY_NAME` - the name of repository;
* `IS_CONTAINER` - true if publishing into repository;
* `ID` - id of container, default: empty;
* `PLATFORM_NAME` - the name of platform;
* `REGENERATE_METADATA` - true if regenerate metadata of repository.

### Template of script

    #!/bin/sh
    echo '--> <platform_type>-scripts/publish-packages: build.sh'

    released="$RELEASED"
    rep_name="$REPOSITORY_NAME"
    is_container="$IS_CONTAINER"
    id="$ID"
    platform_name="$PLATFORM_NAME"
    regenerate_metadata="$REGENERATE_METADATA"

    # Default folders
    # - /home/vagrant/publish-build-list-script
    script_path=/home/vagrant/publish-build-list-script

    # Container path:
    # - /home/vagrant/container
    container_path=/home/vagrant/container

    # /home/vagrant/share_folder contains:
    # - http://abf.rosalinux.ru/downloads/rosa2012.1/repository
    # - http://abf.rosalinux.ru/downloads/akirilenko_personal/repository/rosa2012.1
    repository_path=/home/vagrant/share_folder

    # TODO: Check 'released' status of platform and create all folders
    # status='release'
    # if [ "$released" == 'true' ] ; then
    #  status='updates'
    # fi
    # mkdir -p $repository_path/{SRPMS,i586,x86_64}/$rep_name/$status/repodata

    sign_rpm=0
    gnupg_path=/home/vagrant/.gnupg
    if [ ! -d "$gnupg_path" ]; then
     echo "--> $gnupg_path does not exist"
    else
     sign_rpm=1
     # TODO: Initialize scripts and etc for sign packages
     # keys have name: pubring.gpg and secring.gpg
     # /bin/bash $script_path/init_rpmmacros.sh
    fi

    arches="SRPMS i586 x86_64"
    file_store_url='http://file-store.rosalinux.ru/api/v1/file_stores'
    for arch in $arches ; do
     # TODO: Create all folders
     # TODO: Create backup of repodata

     new_packages="$container_path/new.$arch.list"
     if [ -f "$new_packages" ]; then
       cd $rpm_new
       for sha1 in `cat $new_packages` ; do
         # TODO: Download new package from File-Store by “sha1”
         # TODO: sign new package
       done
     fi

     # TODO: Create backup of old packages, remove old packages
     # TODO: use “continue” If no new packages and no packages for remove

     if [ "$regenerate_metadata" != 'true' ] ; then
       # TODO: Regenerate metadata of repository
     else
       # TODO: Update metadata of repository
     fi

     # Check exit code and “break” if something wrong
     if [ $rc != 0 ] ; then
       break
     fi

     if [ "$is_container" == 'true' ] ; then
       # TODO: Build something else for container if needed
     fi

    done

    # Check exit code after build and rollback
    if [ $rc != 0 ] ; then
     RELEASED=$released REPOSITORY_NAME=$rep_name USE_FILE_STORE=false /bin/bash $script_path/rollback.sh
    else
     # TODO: Remove backup folders and etc.
    fi

    exit $rc

## rollback.sh script

`rollback.sh` uses for rollback publishing packages and regenerating metadata when something went wrong.

### Input parameters:

  * `RELEASED` - realise status of platform;
  * `REPOSITORY_NAME` - the name of repository;
  * `USE_FILE_STORE` - true if called from `build.sh`.


### Template of script

    #!/bin/sh
    echo '--> <platform_type>-scripts/publish-packages: rollback.sh'

    released="$RELEASED"
    rep_name="$REPOSITORY_NAME"
    use_file_store="$USE_FILE_STORE"

    # Container path:
    # - /home/vagrant/container
    container_path=/home/vagrant/container
    repository_path=/home/vagrant/share_folder

    for arch in SRPMS i586 x86_64 ; do
     # TODO: Apply backups and remove new packages from repository
     # TODO: Remove backup folders and etc.
    done

    exit 0

## resign.sh script

`resign.sh` uses for sign all packages in repository.

### Input parameters:

  * `RELEASED` - realise status of platform;
  * `REPOSITORY_NAME` - the name of repository.

### Template of script

    #!/bin/sh
    echo '--> <platform_type>-scripts/publish-packages: resign.sh'

    released="$RELEASED"
    rep_name="$REPOSITORY_NAME"

    # /home/vagrant/share_folder contains:
    # - http://abf.rosalinux.ru/downloads/rosa2012.1/repository
    repository_path=/home/vagrant/share_folder

    # Current path:
    # - /home/vagrant/publish-build-list-script
    script_path=/home/vagrant/publish-build-list-script

    gnupg_path=/home/vagrant/.gnupg
    if [ ! -d "$gnupg_path" ]; then
     echo "--> $gnupg_path does not exist"
     exit 0
    fi

    # TODO: Initialize scripts and etc for sign packages
    # keys have name: pubring.gpg and secring.gpg
    # /bin/bash $script_path/init_rpmmacros.sh

    for arch in SRPMS i586 x86_64 ; do
      # TODO: Sign all packages in remository
    done

    exit 0


## Return codes:

  * `0` - build has been done successfully;
  * `1` - build has been failed;