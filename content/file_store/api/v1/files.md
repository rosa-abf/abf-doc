---
title: Files | File Store API Documentation
---

# Files API

* <a href="#create-file">Create a File </a>
* <a href="#find-a-file">Find a File</a>
* <a href="#get-a-file">Get a File</a>
* <a href="#destroy-file">Destroy File</a>

## Create file

<pre>POST <strong>http://file-store.rosalinux.ru</strong>/api/v1/upload</pre>

### Input:

file_store[file]:
: _Required_ file.

### Request example:

<pre class="terminal">
$ curl --user myuser@gmail.com:mypass -POST -F "file_store[file]=@/path/to/file/archive.zip" http://file-store.rosalinux.ru/api/v1/upload
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

## Destroy file

Users are only able to delete their own files.

<pre>DELETE <strong>http://file-store.rosalinux.ru</strong>/api/v1/file_stores/:hash.json</pre>

### Parameters:

hash
: _Required_ **String** SHA1 of the file.

### Request example:

<pre class="terminal">
$ curl --user myuser@gmail.com:mypass -X DELETE http://file-store.rosalinux.ru/api/v1/file_stores/3a93e5553490e39b4cd50269d51ad8438b7e20b8.json
</pre>

## Response

  Status: 204 No Content
