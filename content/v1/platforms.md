---
title: Platforms | ABF API
---

# Platforms API

* <a href="#get-a-single-platform">Get a single platform</a>
* <a href="#update-a-single-platform">Update a single platform</a>
* <a href="#members-of-a-single-platform">Members of a single platform</a>
* <a href="#add-member-to-a-single-platform">Add member to a single platform</a>
* <a href="#remove-member-from-a-single-platform">Remove member from a single platform</a>
* <a href="#clone-of-a-single-platform">Clone of a single platform</a>
* <a href="#list-platforms">List platforms</a>

## Get a single platform

    GET /api/v1/platforms/:id.json

### Parameters:

id
: _Integer_ identifier of current platform

### Response:

<%= json(:platform_data_response) %>

### Example:

<%= json(:platform_data_response_example) %>

## Update a single platform

	PUT /api/v1/platforms/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

description:
: _Optional_ **String** platform description

released:
: _Optional_ **Boolean** realise status of platform

owner_id:
: _Optional_ **Integer** identifier of platform owner

### Request:

<%= json(:platform_update_request) %>

### Response:

<%= json(:platform_update_response) %>

### Example:

<%= json(:platform_update_response_example) %>

## Members of a single platform

	GET /api/v1/platforms/:id/members.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Request example:

    /api/v1/platforms/53/members.json

### Response:

<%= json(:platform_members_response) %>

### Example:

<%= json(:platform_members_response_example) %>

## Add member to a single platform

	GET /api/v1/platforms/:id/add_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

member_id
: _Required_ **Integer** identifier of new member

type
: _Required_ **String** `Group` or `User` type of new member

### Request:

<%= json(:platform_add_member_request) %>

### Response:

<%= json(:platform_add_member_response) %>

### Examples:

<%= json(:platform_add_member_response_example) %>

&nbsp;

<%= json(:platform_add_member_response_example2) %>

## Remove member from a single platform

    GET /api/v1/platforms/:id/remove_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

member_id
: _Required_ **Integer** identifier of member

type
: _Required_ **String** `Group` or `User` type of member

### Request:

<%= json(:platform_remove_member_request) %>

### Response:

<%= json(:platform_remove_member_response) %>

### Examples:

<%= json(:platform_remove_member_response_example) %>

&nbsp;

<%= json(:platform_remove_member_response_example2) %>

## Clone of a single platform

    POST /api/v1/platforms/:id/clone.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

description:
: _Required_ **String** platform description

name:
: _Required_ **String** platform name

### Request:

<%= json(:platform_clone_request) %>

### Response:

<%= json(:platform_clone_response) %>

### Examples:

<%= json(:platform_clone_response_example) %>

## List platforms

    GET /api/v1/platforms.json

### Parameters:

type
: _Optional_ filter platforms by type: `main` or `personal`. Also you can don't set the type to get all of the platforms

### Request examples:

    /api/v1/platforms.json?type=main
    /api/v1/platforms.json?type=personal
    /api/v1/platforms.json

### Response:

<%= json(:platform_list_response) %>

### Example:

<%= json(:platform_list_response_example) %>

