---
title: Repositories | ABF API
---

# Repositories API

* <a href="#get-a-single-repository">Get a single repository</a>
* <a href="#list-repositories">List repositories</a>

## Get a single repository

    GET /api/v1/repositories/:id.json

### Parameters:

id
: _Integer_ identifier of current repository

### Response:

<%= json(:repository_data_response) %>

### Example:

<%= json(:repository_data_response_example) %>

## List repositories

    GET /api/v1/repositories.json

### Parameters:

platform_id
: _Required_ **integer** identifier of platform

### Request

<%= json(:repository_list_request) %>

### Response:

<%= json(:repository_list_response) %>

### Example:

<%= json(:repository_list_response_example) %>