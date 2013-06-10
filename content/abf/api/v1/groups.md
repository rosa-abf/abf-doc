---
title: Groups | ABF API
---

# Groups API

* [List groups](#list-groups)
* [Get a single group](#get-a-single-group)
* [Update a single group](#update-a-single-group)
* [Create group](#create-group)
* [Destroy group](#destroy-group)
* [Members of a single group](#members-of-a-single-group)
* [Add member to a single group](#add-member-to-a-single-group)
* [Remove member from a single group](#remove-member-from-a-single-group)
* [Update member role for a single group](#update-member-role-for-a-single-group)

## List groups

List all the authenticated user’s groups including owned groups and member groups.

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

## Add member to a single group

    PUT /api/v1/groups/:id/add_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Input:

member_id
: _Required_ **Integer** identifier of new member (may be added only `User`).

role
: _Optional_ **String** role for new member (`reader`/`writer`/`admin`), by default `admin`.

### Request:

<%= json(:group_add_member_request) %>

### Response:

<%= json(:group_add_member_response) %>

### Examples:

<%= json(:group_add_member_response_example) %>

## Remove member from a single group

    DELETE /api/v1/groups/:id/remove_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Input:

member_id
: _Required_ **Integer** identifier of member (may be removed only `User`).

### Request:

<%= json(:group_remove_member_request) %>

### Response:

<%= json(:group_remove_member_response) %>

### Examples:

<%= json(:group_remove_member_response_example) %>

## Update member role for a single group

    PUT /api/v1/groups/:id/update_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current group.

### Input:

member_id
: _Required_ **Integer** identifier of member.

role
: _Required_ **String** new role for member (`reader`, `writer`, `admin`).

### Request:

<%= json(:group_update_member_request) %>

### Response:

<%= json(:group_update_member_response) %>

### Examples:

<%= json(:group_update_member_response_example) %>
