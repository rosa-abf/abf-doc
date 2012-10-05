---
title: Repositories | ABF API
---

# Repositories API

* <a href="#get-a-single-repository">Get a single repository</a>
* <a href="#list-repositories">List repositories</a>
* <a href="#update-a-single-repository">Update a single repository</a>
* <a href="#create-repository">Create repository</a>
* <a href="#destroy-repository">Destroy repository</a>

## Get a single repository

    GET /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Response:

<%= json(:repository_data_response) %>

### Example:

<%= json(:repository_data_response_example) %>

## List repositories

    GET /api/v1/repositories.json

### Parameters:

platform_id
: _Required_ **Integer** identifier of platform.

### Request:

<%= json(:repository_list_request) %>

### Response:

<%= json(:repository_list_response) %>

### Example:

<%= json(:repository_list_response_example) %>

## Update a single repository

    PUT /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

description:
: _Optional_ **String** repository description.

publish_without_qa:
: _Optional_ **Boolean** status of publication without QA.

### Request:

<%= json(:repository_update_request) %>

### Response:

<%= json(:repository_update_response) %>

### Example:

<%= json(:repository_update_response_example) %>

## Create repository

    POST /api/v1/repositories/:id.json

### Parameters:

platform_id
: _Required_ **Integer** identifier of platform.

description:
: _Required_ **String** repository description.

name:
: _Required_ **String** repository name.

publish_without_qa:
: _Optional_ **Boolean** status of publication without QA. Default: `true`.

### Request:

<%= json(:repository_create_request) %>

### Response:

<%= json(:repository_create_response) %>

### Example:

<%= json(:repository_create_response_example) %>

## Destroy repository

    DELETE /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Response:

<%= json(:repository_destroy_response) %>

### Example:

<%= json(:repository_destroy_response_example) %>