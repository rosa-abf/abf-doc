---
title: Repositories | ABF API
---

# Repositories API

* [Get a single repository](#get-a-single-repository)
* [Projects of a single repository](#projects-of-a-single-repository)
* [Update a single repository](#update-a-single-repository)
* [Create repository](#create-repository)
* [Destroy repository](#destroy-repository)
* [Add member to a single repository](#add-member-to-a-single-repository)
* [Remove member from a single repository](#remove-member-from-a-single-repository)
* [Add project to a single repository](#add-project-to-a-single-repository)
* [Remove project from a single repository](#remove-project-from-a-single-repository)
* [Update signatures for a single repository](#update-signatures-for-a-single-repository)

## Get a single repository

    GET /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Response:

<%= json(:repository_data_response) %>

### Example:

<%= json(:repository_data_response_example) %>

## Projects of a single repository

    GET /api/v1/repositories/:id/projects.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Response:

<%= json(:repository_projects_response) %>

### Example:

<%= json(:repository_projects_response_example) %>

## Update a single repository

    PUT /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Input:

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

    POST /api/v1/repositories.json

### Input:

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
A repository with `main` name can't be deleted from `personal` platform.

    DELETE /api/v1/repositories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository.

### Response:

<%= json(:repository_destroy_response) %>

### Example:

<%= json(:repository_destroy_response_example) %>

## Add member to a single repository
Only for repositories from `main` platform.

	PUT /api/v1/repositories/:id/add_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository

### Input:

member_id
: _Required_ **Integer** identifier of new member

type
: _Required_ **String** `Group` or `User` type of new member

### Request:

<%= json(:repository_add_member_request) %>

### Response:

<%= json(:repository_add_member_response) %>

### Examples:

<%= json(:repository_add_member_response_example) %>

&nbsp;

<%= json(:repository_add_member_response_example2) %>

## Remove member from a single repository
Only for repositories from `main` platform.

    DELETE /api/v1/repositories/:id/remove_member.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository

### Input:

member_id
: _Required_ **Integer** identifier of member

type
: _Required_ **String** `Group` or `User` type of member

### Request:

<%= json(:repository_remove_member_request) %>

### Response:

<%= json(:repository_remove_member_response) %>

### Examples:

<%= json(:repository_remove_member_response_example) %>

&nbsp;

<%= json(:repository_remove_member_response_example2) %>

## Add project to a single repository

	PUT /api/v1/repositories/:id/add_project.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository

### Input:

project_id
: _Required_ **Integer** identifier of project

### Request:

<%= json(:repository_add_project_request) %>

### Response:

<%= json(:repository_add_project_response) %>

### Examples:

<%= json(:repository_add_project_response_example) %>

## Remove project from a single repository

    DELETE /api/v1/repositories/:id/remove_project.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository

### Input:

project_id
: _Required_ **Integer** identifier of project

### Request:

<%= json(:repository_remove_project_request) %>

### Response:

<%= json(:repository_remove_project_response) %>

### Examples:

<%= json(:repository_remove_project_response_example) %>

## Update signatures for a single repository
Only for repositories from `main` platform.

    PUT /api/v1/repositories/:id/signatures.json

### Parameters:

id
: _Required_ **Integer** identifier of current repository

### Input:

public
: _Required_ **String** public key

secret
: _Required_ **String** secret key

### Request:

<%= json(:repository_signatures_request) %>

### Response:

<%= json(:repository_signatures_response) %>

### Examples:

<%= json(:repository_signatures_response_example) %>