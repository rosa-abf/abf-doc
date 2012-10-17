---
title: Projects | ABF API
---

# Projects API

* <a href="#list-projects">List projects</a>
* <a href="#get-a-single-project">Get a single project</a>
* <a href="#get-project-id">Get project id</a>
* <a href="#get-all-references-of-project">Get all references of project</a>
* <a href="#update-a-single-project">Update a single project</a>
* <a href="#create-project">Create project</a>
* <a href="#destroy-project">Destroy project</a>
* <a href="#fork-project">Fork project</a>
* <a href="#members-of-a-single-project">Members of a single project</a>
* <a href="#add-member-to-a-single-project">Add member to a single project</a>
* <a href="#remove-member-from-a-single-project">Remove member from a single project</a>
* <a href="#update-member-role-for-a-single-project">Update member role for a single project</a>

## List projects

    GET /api/v1/projects.json

### Response:

<%= json(:project_list_response) %>

### Example:

<%= json(:project_list_response_example) %>

## Get a single project

    GET /api/v1/projects/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

### Response:

<%= json(:project_data_response) %>

### Example:

<%= json(:project_data_response_example) %>

## Get project id

    GET /api/v1/projects/get_id.json?name=:project_name&owner=:owner_name

### Parameters:

project_name
: _String_ project name.

owner_name: 
: _String_ project owner name.

### Request examples:

    /api/v1/projects/get_id.json?name=rails&owner=warpc

### Response:

<%= json(:project_get_id_response) %>

### Example:

<%= json(:project_get_id_response_example) %>

## Get all references of project

    GET /api/v1/projects/:id/refs_list.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

### Response:

<%= json(:project_refs_list_response) %>

### Example:

<%= json(:project_refs_list_response_example) %>

## Update a single project

  PUT /api/v1/projects/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

### Input:

description:
: _Optional_ **String** project description.

visibility:
: _Optional_ **String** project visibility (`open`/`hidden`).

is_package:
: _Optional_ **Boolean** `true` if project is package.

default_branch:
: _Optional_ **String** project default branch.

has_issues:
: _Optional_ **Boolean** enable/disable project Issues tracker.

has_wiki:
: _Optional_ **Boolean** enable/disable project wiki.

maintainer_id:
: _Optional_ **Integer** identifier of project maintainer.

### Request:

<%= json(:project_update_request) %>

### Response:

<%= json(:project_update_response) %>

### Example:

<%= json(:project_update_response_example) %>

## Create project

    POST /api/v1/projects.json

### Input:

name:
: _Required_ **String** project name.

owner_id:
: _Required_ **Integer** identifier of project owner.

owner_type:
: _Required_ **String** type of project owner.

visibility:
: _Required_ **String** project visibility (`open`/`hidden`).

description:
: _Optional_ **String** project description.

is_package:
: _Optional_ **Boolean** `true` if project is package.

default_branch:
: _Optional_ **String** project default branch.

has_issues:
: _Optional_ **Boolean** enable/disable project Issues tracker.

has_wiki:
: _Optional_ **Boolean** enable/disable project wiki.

maintainer_id:
: _Optional_ **Integer** identifier of project maintainer.

### Request:

<%= json(:project_create_request) %>

### Response:

<%= json(:project_create_response) %>

### Examples:

<%= json(:project_create_response_example) %>