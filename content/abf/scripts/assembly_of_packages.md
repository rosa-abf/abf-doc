---
title: RosaLab ABF Documentation - Assembly of packages
---

# RosaLab ABF Documentation - Assembly of packages

* <a href="#introduction">Introduction</a>
* <a href="#input-parameters">Input parameters</a>
* <a href="#template-of-script">Template of script</a>
* <a href="#return-codes">Return codes</a>

## Introduction

Different scripts uses for each type of platform. If You would like to create new script, we recommend to review next projects:

* <a href="https://abf.rosalinux.ru/abf/rhel-scripts/tree/master/build-packages">RHEL scripts</a>
* <a href="https://abf.rosalinux.ru/abf/mdv-scripts/tree/master/build-packages">MDV scripts</a>

It contains scripts for MDV and RHEL platforms.


## Input parameters:

  * `GIT_PROJECT_ADDRESS` - GIT url of project;
  * `COMMIT_HASH` - commit hash of project;
  * `UNAME` - uname of user which build the project;
  * `EMAIL` - email of user which build the project;
  * `PLATFORM_NAME` - name of platform for which project will be built;
  * `ARCH` - arch of platform for which project will be built.

## Template of script

    #!/bin/sh

    echo '--> <platform_type>-scripts/build-packages: build.sh'

    git_project_address="$GIT_PROJECT_ADDRESS"
    commit_hash="$COMMIT_HASH"
    uname="$UNAME"
    email="$EMAIL"
    platform_name="$PLATFORM_NAME"
    platform_arch="$ARCH"

    # Default folders
    results_path="/home/vagrant/results"
    tmpfs_path="/home/vagrant/tmpfs"
    project_path="$tmpfs_path/project"
    rpm_build_script_path=`pwd`

    rm -rf $results_path $tmpfs_path $project_path
    mkdir  $results_path $tmpfs_path $project_path

    # Mount tmpfs
    sudo mount -t tmpfs tmpfs -o size=30000M,nr_inodes=10M $tmpfs_path

    # Download project
    # Fix for: 'fatal: index-pack failed'
    git config --global core.compression -1
    git clone $git_project_address $project_path && cd $project_path
    git remote rm origin && git checkout $commit_hash

    # TODO: Build changelog
    # TODO: Downloads extra files by .abf.yml

    # Remove .git folder
    rm -rf $project_path/.git

    # TODO: Build packages
    # TODO: Move logs into “results_path”
    # use: “exit 1” if build failed
    # TODO: Run tests of new packages and set “test_code” variable:
    # - 0 if tests passed;
    # - 1 if tests failed.

    # TODO: Generate "$results_path/container_data.json"
    # file which will be contain all information about new packages.
    # Only packages which will be described in this file will be
    # interpreted as "packages"!!!
    # "container_data.json" looks as:
    # [
    #   {
    #     “fullname”:”fullname of package”,
    #     “sha1”:”sha1 of package”,
    #     “name”:”name of package file”,
    #     “version”:”version of package”,
    #     “release”:”release of package”
    #   },
    #   ...
    # ]
    # TODO: Move all packages into results folder (“$results_path”)

    # Umount tmpfs
    cd /; sudo umount $tmpfs_path; rm -rf $tmpfs_path

    # Check exit code after testing
    if [ $test_code != 0 ] ; then
     echo '--> Test failed!'
     exit 5
    fi
    echo '--> Build has been done successfully!'
    exit 0

## Return codes:

  * `0` - build has been done successfully;
  * `1` - build has been failed;
  * `5` - tests failed.
