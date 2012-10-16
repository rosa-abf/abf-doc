---
title: Groups | ABF API
---

# Groups API

* <a href="#list-groups">List groups</a>
* <a href="#get-a-single-group">Get a single group</a>
* <a href="#update-a-single-group">Update a single group</a>
* <a href="#create-group">Create group</a>
* <a href="#destroy-group">Destroy group</a>
* <a href="#users-of-a-single-group">Users of a single group</a>
* <a href="#add-user-to-a-single-group">Add user to a single group</a>
* <a href="#remove-user-from-a-single-group">Remove user from a single group</a>
* <a href="#update-user-role-for-a-single-group">Update user role for a single group</a>

## List groups

    GET /api/v1/groups.json

### Response:

<%= json(:group_list_response) %>

### Example:

<%= json(:group_list_response_example) %>

## Get a single group

    GET /api/v1/groups/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Response:

<%= json(:group_data_response) %>

### Example:

<%= json(:group_data_response_example) %>

## Update a single group

  PUT /api/v1/groups/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current group

### Input:

description:
: _Optional_ **String** group description

### Request:

<%= json(:group_update_request) %>

### Response:

<%= json(:group_update_response) %>

### Example:

<%= json(:group_update_response_example) %>