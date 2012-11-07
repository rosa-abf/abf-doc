---
title: File Store | ABF API
---

# File Store API

* <a href="#create-file">Create a File </a>
* <a href="#find-a-file">Find a File</a>
* <a href="#get-a-file">Get a File</a>

## Create file

<pre>POST <strong>http://file-store.rosalinux.ru</strong>/api/v1/file_stores.json</pre>

### Input:

file_store[file]:
: _Required_ file.

### Request:

<pre class="terminal">
$ curl --user myuser@gmail.com:mypass -POST -F "file_store[file]=@files/archive.zip" http://file-store.rosalinux.ru/api/v1/file_stores.json
</pre>

### Response:

<%= json(:file_store_create_response) %>

### Examples:

<%= json(:file_store_create_response_example) %>

## Find a File

<pre>GET <strong>http://file-store.rosalinux.ru</strong>/api/v1/file_stores.json?hash=:hash</pre>

### Parameters:

hash
: _Required_ **String** hash of the file.

### Response:

<%= json(:file_store_find_response) %>

### Example:

<%= json(:file_store_find_response_example) %>

## Get a File

<pre>GET <strong>http://file-store.rosalinux.ru</strong>/api/v1/file_stores/:hash</pre>

### Parameters:

hash
: _Required_ **String** SHA1 of the file.

### Response:

File content

