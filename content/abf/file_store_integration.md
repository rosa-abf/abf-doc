---
title: RosaLab ABF Integration with FileStore (.abf.yml)
---

# Integration with FileStore (.abf.yml)

* <a href="#abfyml-file-what-it-is-and-how-it-is-used">.abf.yml file: what it is and how it is used</a>
* <a href="#how-it-use">How it use?</a>

## .abf.yml file: what it is and how it is used

ABF uses `.abf.yml` file in the root of your repository to learn about your project and which extra files should be present in the project. `.abf.yml` can be very minimalistic.

`.abf.yml` contains SHA1 of extra files which have been saved on the
<a href="http://file-store.rosalinux.ru/">File-Store</a>
and it is great, because we have a light git repository with code and
<a href="http://file-store.rosalinux.ru/">File-Store</a>
with some BIG archives and files.

Our ABF build services have ability to download all extra files by `.abf.yml`.

`.abf.yml` has very easy format, <a href="http://en.wikipedia.org/wiki/YAML">YAML</a> format:

    sources:
      "<file name 1>": <sha1 of file 1>
      "<file name 2>": <sha1 of file 2>  
      …
      "<file name n>": <sha1 of file n>

## How it use?

Your git repository contains some BIG files (archives, binary files and etc.).<br/>
First of all You should upload big files into
<a href="http://file-store.rosalinux.ru/">File-Store</a>.<br/>
So, You have file names and sha1 of files.<br/>
After You should add `.abf.yml` file into repository. `.abf.yml` will look as:

    sources:
      "at_3.1.12.orig.tar.gz": 1cf47df152e9d119e083c11eefaf6368c993a8af
      "gnome-control-center-2.32.1.tar.bz2": 1e5ba3117aba7f939de25dbed13e430b90968561

### Important:
* we suggest to write filename in quotes;
* sha1 should not be in quotes;
* spaces should not exist before sources;
* 2 spaces should be exist before “file_name”;
* the name of file should be easy (not use quotes, %, ^ and etc.)
