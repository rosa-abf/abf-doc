---
title: Users | ABF API
---

# Users API

* <a href="#get-a-single-user">Get a single user</a>
* <a href="#update-a-single-user">Update a single user</a>

## Get a single user

    GET /api/v1/users/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current user.

### Response:

<%= json(:user_data_response) %>

### Example:

<%= json(:user_data_response_example) %>

## Update a single user

    PUT /api/v1/users/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current user.

### Input:

description:
: _Optional_ **String** repository description.

publish_without_qa:
: _Optional_ **Boolean** status of publication without QA.

### Request:

<%= json(:user_update_request) %>

### Response:

<%= json(:user_update_response) %>

### Example:

<%= json(:user_update_response_example) %>