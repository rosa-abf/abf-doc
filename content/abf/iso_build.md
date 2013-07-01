---
title: ISO build environment | ABF Documentation
---

# ISO build environment

* [Prerequisites and restrictions](#prerequisites-and-restrictions)
* [Building the product and creating the ISO disk image](#building-the-product-and-creating-the-iso-disk-image)
* [The Virtual Machine and the build process details](#the-virtual-machine-and-the-build-process-details)

## Prerequisites and restrictions

- The product can be built for the main platform only;
- The user must have all necessary permissions to build the product.

## Building the product and creating the ISO disk image

1\. Navigate to the platform menu, select the `Products` menu entry and press the `New product`button:

![Show products](/images/products.png)

Enter the following information into the form:

- product name;
- product description;
- project containing the build scripts;
- entry point i.e. the bash script used to build the main product;
- the bash script arguments needed to build the product;
- the maximum amount of time needed to build the product.

2\. The above parameters will be used as the default parameters for building the product `ProductBuildList`.

![New product](/images/product_new.png)

Press the `Save` button.

3\. After the default setting are saved you'll be transferred to the product page where you can create the `ProductBuildList` or ISO image

![Show product](/images/product_show.png)

4\. Press the `Build` button to open the form for the product build task or the ISO image creating task

![Show product](/images/product_build_list_new.png)

Enter the following information into the form:

- your build script project branch;
- the main file containing bash script used to build the product;
- the script arguments;
- maximum amount of time needed to build the product.

## The Virtual Machine and the build process details

1\. You will operate under `vagrant` user account

2\. The following working directories will be created by default:

- `/home/vagrant/results` after finishing the build process all files from this directory are saved on a [File-Store](http://file-store.rosalinux.ru/), and the downloading links
will be available on a build review page at the `Results` ABF section (recommended place for storing the build logs and ISO disk images);
- `/home/vagrant/archives` after the build process is finished, this directory will be archived into the `/home/vagrant/results` directory (recommended place for storing secondary information which will be available in the form of single archive file after the build);
- `/home/vagrant/iso_builder` this is tmpfs directory with the size of `30.000MB` where all your project files will be stored. It is strictly recommended to use this directory in your build script (for creating temporary files etc).

### NOTE:

- any data created outside the `/home/vagrant/results` and `/home/vagrant/archives` won't be available after the build process is finished;
- the amount of free disk space of the virtual machine is around `9GB` so please consider it while saving the results.

3\. The virtual machine has a minimal set of system packages installed, so you'll have to install all additional programs needed for your build process. Remember that the architecture is `x86_64`.

4\. Your script will be run (with the arguments specified) under user `vagrant` from directory `/home/vagrant/iso_builder`. For example:

    cd iso_builder/; <Params for running script> /bin/bash <Main script>

### NOTE:

- your script may contain root commands (sudo <command name>);
- the directory `iso_builder` will contain the build project version specified during the build setup. It means that only the specified version will be downloaded into the directory and NOT the whole project. (The `.git` directory won't be available and you won't be able to switch to another branch of the project in your script).

5\. Every build is performed within it's own virtual machine. After the build is done the machine will be reset to its defaults.

6\. In case if the maximum amount of build time (`Max time for building (in minutes)`) is exceeded, the build will be canceled and the virtual machine rollback will be performed. No VM data will be saved and "Product build list" will receive exit status of `Build canceled`.

7\. The VM is connected to the Internet so you can download/upload any additional data and the final results from within your script (in case you do not want to use the default settings for those operations).

8\. The zero build process exit code means success, any other exit code will be interpreted as a build error.

9\. The table shows how the build result depends on build status

| __Condition__  | __Results are saved__ |
|:----------|:-----------------:|
| The build script returned any exit code (0,1, ...) | + |
| The build was canceled by user | - |
| The build was canceled by system (max build time exceeded) | - |
