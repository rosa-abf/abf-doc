---
title: Integration with FileStore (.abf.yml) | ABF Documentation
---

# Integration with FileStore (.abf.yml)

* [.abf.yml file: what it is and how it is used](#abfyml-file-what-it-is-and-how-it-is-used)
* [How it use?](#how-it-use)

## .abf.yml file: what it is and how it is used

ABF uses `.abf.yml` file in the root of your repository to learn about your project and which extra files should be present in the project. `.abf.yml` can be very minimalistic.

`.abf.yml` contains SHA1 of extra files which have been saved on the
[File-Store](http://file-store.rosalinux.ru/)
and it is great, because we have a light git repository with code and
[File-Store](http://file-store.rosalinux.ru/)
with some BIG archives and files.

`.abf.yml` has very easy format, [YAML](http://en.wikipedia.org/wiki/YAML) format:

    sources:
      "<file name 1>": <sha1 of file 1>
      "<file name 2>": <sha1 of file 2>  
      …
      "<file name n>": <sha1 of file n>

Our ABF build services have ability to parse `.abf.yml` file and download all extra files from [File-Store](http://file-store.rosalinux.ru/) by `sha1` (This uses only for build packages).
When file will be downloaded it will be renamed to `file name` from YML file.
Command for downloading looks like:

    curl -L http://file-store.rosalinux.ru/api/v1/file_stores/<sha1> -o <file name>

### Important:
* if file does not exist on File-Store, it will be contain:
    `{"Error 404":["Resource not found!"]}`

* downloading of files occur before building the package (on spade-work);
* build will be go next notwithstanding the fact that some files have not been downloaded;
* information about downloading of files contains in the main log:
    `abfworker::rpm-worker-<build id>.log`

## How it use?

Your git repository contains some BIG files (archives, binary files and etc.).<br/>
First of all you should upload big files into
[File-Store](http://file-store.rosalinux.ru/).<br/>
So, you have file names and sha1 of files.<br/>
After you should add `.abf.yml` file into repository. `.abf.yml` will look as:

    sources:
      "at_3.1.12.orig.tar.gz": 1cf47df152e9d119e083c11eefaf6368c993a8af
      "gnome-control-center-2.32.1.tar.bz2": 1e5ba3117aba7f939de25dbed13e430b90968561

### Important:
* we suggest to write filename in quotes;
* sha1 should not be in quotes;
* spaces should not exist before sources;
* 2 spaces should be exist before “file_name”;
* the name of file should be easy (not use quotes, %, ^ and etc.)
