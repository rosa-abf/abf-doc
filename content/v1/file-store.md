---
title: File Store | ABF API
---

# File Store API

* <a href="#create">Create a File </a>
* <a href="#get">Find a File</a>
* <a href="#send">Get a File</a>

## Create file

<pre>POST <strong>http://file-store.rosalinux.ru</strong>/api/v1/file-stores.json</pre>

### Input:

file_store:
: _Required_ **base64** file content.

file_name:
: _Required_ **String** file name.

### Request:

<%= json(:file_store_create) %>

### Response:

<%= json(:file_store_create_response) %>

### Examples:

<%= json(:file_store_create_response_example) %>

## Find a File

<pre>GET <strong>http://file-store.rosalinux.ru</strong>/api/v1/file-stores.json?hash=:hash</pre>

### Parameters:

hash
: _Required_ **String** hash of the file.

### Response:

<%= json(:file_store_find_response) %>

### Example:

<%= json(:file_store_find_response_example) %>

## Get a File

<pre>GET <strong>http://file-store.rosalinux.ru</strong>/api/v1/file-stores/:hash</pre>

### Parameters:

hash
: _Required_ **String** SHA1 of the file.

### Response:

File content

