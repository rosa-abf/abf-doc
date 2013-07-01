---
title: Platforms | ABF API
---

# Platforms API

* [Get a single platform](#get-a-single-platform)
* [Update a single platform](#update-a-single-platform)
* [Members of a single platform](#members-of-a-single-platform)
* [Add member to a single platform](#add-member-to-a-single-platform)
* [Remove member from a single platform](#remove-member-from-a-single-platform)
* [Clone a single platform](#clone-a-single-platform)
* [Clear a single platform](#clear-a-single-platform)
* [Create platform](#create-platform)
* [Destroy platform](#destroy-platform)
* [List platforms](#list-platforms)
* [List of platforms for which you can create build list](#list-of-platforms-for-which-you-can-create-build-list)

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

### Input:

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

	PUT /api/v1/platforms/:id/add_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Input:

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

    DELETE /api/v1/platforms/:id/remove_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Input:

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

## Clone a single platform

    POST /api/v1/platforms/:id/clone.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Input:

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

## Clear a single platform
Only for `personal` platforms!

    PUT /api/v1/platforms/:id/clear.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Request example:

    /api/v1/platforms/54/clear.json

### Response:

<%= json(:platform_clear_response) %>

### Examples:

<%= json(:platform_clear_response_example) %>

## Create platform

    POST /api/v1/platforms.json

### Input:

name:
: _Required_ **String** platform name

description:
: _Required_ **String** platform description

distrib_type:
: _Required_ **String** distrib_type of platform (`mdv` or `rhel`)

released:
: _Optional_ **Boolean** realise status of platform

owner_id:
: _Optional_ **Integer** identifier of platform owner

### Request:

<%= json(:platform_create_request) %>

### Response:

<%= json(:platform_create_response) %>

### Examples:

<%= json(:platform_create_response_example) %>

## Destroy platform
Only for `main` platforms!

    DELETE /api/v1/platforms/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

### Request example:

    /api/v1/platforms/54.json

### Response:

<%= json(:platform_destroy_response) %>

### Examples:

<%= json(:platform_destroy_response_example) %>

## List platforms

List all platforms across all the authenticated user’s platforms including owned platforms, member platforms, and group platforms.

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

## List of platforms for which you can create build list.
This data required for api [Сreate build list](/abf/api/v1/build_lists/#create-build-list).

    GET /api/v1/platforms/platforms_for_build.json

### Request examples:

    /api/v1/platforms/platforms_for_build.json

### Response:

<%= json(:platform_for_build_response) %>

### Example:

<%= json(:platform_for_build_response_example) %>
