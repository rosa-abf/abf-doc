---
title: Groups | ABF API
---

# Groups API

* <a href="#list-groups">List groups</a>
* <a href="#get-a-single-group">Get a single group</a>
* <a href="#update-a-single-group">Update a single group</a>
* <a href="#create-group">Create group</a>
* <a href="#destroy-group">Destroy group</a>
* <a href="#users-of-a-single-group">Members of a single group</a>
* <a href="#add-member-to-a-single-group">Add member to a single group</a>
* <a href="#remove-member-from-a-single-group">Remove member from a single group</a>
* <a href="#update-member-role-for-a-single-group">Update member role for a single group</a>

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
: _Required_ **Integer** identifier of current group.

### Input:

description:
: _Optional_ **String** group description.

### Request:

<%= json(:group_update_request) %>

### Response:

<%= json(:group_update_response) %>

### Example:

<%= json(:group_update_response_example) %>

## Create group

    POST /api/v1/groups.json

### Input:

uname:
: _Required_ **String** group uname.

description:
: _Optional_ **String** group description.

### Request:

<%= json(:group_create_request) %>

### Response:

<%= json(:group_create_response) %>

### Examples:

<%= json(:group_create_response_example) %>

## Destroy group

    DELETE /api/v1/groups/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Request example:

    /api/v1/groups/54.json

### Response:

<%= json(:group_destroy_response) %>

### Examples:

<%= json(:group_destroy_response_example) %>

## Members of a single group

    GET /api/v1/groups/:id/members.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Response:

<%= json(:group_members_response) %>

### Example:

<%= json(:group_members_response_example) %>