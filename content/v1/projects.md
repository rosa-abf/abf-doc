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
: _Required_ **Integer** identifier of current project

### Response:

<%= json(:project_data_response) %>

### Example:

<%= json(:project_data_response_example) %>

## Get project id

    GET /api/v1/projects/get_id.json?name=:project_name&owner=:owner_name

### Parameters:

project_name
: _String_ project name

owner_name: 
: _String_ project owner name

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
: _Required_ **Integer** identifier of current project

### Response:

<%= json(:project_refs_list_response) %>

### Example:

<%= json(:project_refs_list_response_example) %>