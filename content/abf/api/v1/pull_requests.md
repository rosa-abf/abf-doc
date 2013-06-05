---
title: Pull Requests | ABF API
---

# Pull Requests API

* <a href="#list-pull-requests">List pull requests</a>
* <a href="#list-pull-requests-for-a-project">List pull requests for a project</a>
* <a href="#get-a-single-pull-request">Get a single pull request</a>
* <a href="#create-an-pull-request">Create an pull request</a>
* <a href="#update-a-single-pull-request">Update a single pull request</a>
* <a href="#list-commits-on-a-pull-request">List commits on a pull request</a>
* <a href="#list-pull-requests-files">List pull requests files</a>
* <a href="#merge-a-single-pull-request">Merge a single pull request</a>

## List pull requests

List all pull requests across all the authenticated user’s projects including owned projects, member projects, and group projects:

    GET /api/v1/pull_requests.json

List all pull requests across owned and member projects for the authenticated user:

    GET /api/v1/user/pull_requests.json

List all pull requests for a given group for the authenticated user:

    GET /api/v1/group/:id/pull_requests.json

### Parameters

filter
: _Optional_ **String**
: * `assigned`: Pull requests assigned to you (default)
  * `created`: Pull requests created by you
  * `all`: All pull requests the authenticated user can see

status
: _Optional_ **String** `open` (default), `closed`

sort
: _Optional_ **String** `submitted` (default), `updated`.

direction
: _Optional_ **String** `asc` or `desc` (default).

since
: _Optional_ **Integer** of a timestamp in Unix time format.

### Response:

<%= json(:pull_requests_list_response) %>

### Example:

<%= json(:pull_requests_list_response_example) %>

## List pull requests for a project

    GET /api/v1/projects/:id/pull_requests.json

### Parameters

status
: _Optional_ **String** `open` (default), `closed`

assignee
: _Optional_ **String**
: * _String_ User nickname
  * `none` for Issues with no assigned User.
  * `*` for Issues with any assigned User.

creator
: _Optional_ **String** User nickname.

sort
: _Optional_ **String** `submitted` (default), `updated`.

direction
: _Optional_ **String** `asc` or `desc` (default).

since
: _Optional_ **Integer** of a timestamp in Unix time format.

### Response:

<%= json(:pull_requests_list_response) %>

### Example:

<%= json(:pull_requests_list_response_example) %>

## Get a single pull requests

    GET /api/v1/projects/:project_id/pull_requests/:number.json

### Parameters:

project_id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current pull request.

### Response:

<%= json(:pull_request_data_response) %>

### Example:

<%= json(:pull_request_data_response_example) %>

## Create an pull request

Any authenticated user with read access to a project can create an pull request.

    POST /api/v1/projects/:id/pull_requests.json

### Input

title
: _Required_ **String**

body
: _Required_ **String**

assignee
: _Optional_ **Integer** - Id for the user that this pull request should be
assigned to. _NOTE: Only users with push access can set the assignee for
pull request. The assignee is silently dropped otherwise._

to_ref
: _Required_ **String** the branch (or git ref) you want your changes pulled into.
This should be an existing branch on the current repository.
You cannot submit a pull request to one repo that requests a merge to a base of another repo.

from_project
: _Optional **Integer** Identifier project where your changes are implemented. Default current project.

from_ref
: _Required_ **String** the branch (or git ref) where your changes are implemented.

### Request:

<%= json(:pull_request_create_request) %>

### Response:

<%= json(:pull_request_create_response) %>

### Examples:

<%= json(:pull_request_create_response_example) %>

## Update a single pull request

    PUT /api/v1/projects/:id/pull_requests/:number.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current pull request.

### Input:

title
: _Optional_ **String**

body
: _Optional_ **String**

assignee
: _Optional_ **Integer** - Identifier for the user that this pull request should be
assigned to.

status
: _Optional_ **String** - State of the pull request: `open` or `closed`.

### Request:

<%= json(:pull_request_update_request) %>

### Response:

<%= json(:pull_request_update_response) %>

### Example:

<%= json(:pull_request_update_response_example) %>

## List commits on a pull request

    GET /api/v1/projects/:id/pull_requests/:number.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current pull request.

### Response:

<%= json(:list_commits_pull_request_data_response) %>

### Example:

<%= json(:list_commits_pull_request_data_response_example) %>

## List pull requests files

    GET /api/v1/projects/:id/pull_requests/:number.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current pull request.

### Response:

<%= json(:list_pull_requests_files_data_response) %>

### Example:

<%= json(:list_pull_requests_files_data_response_example) %>

## Merge a pull request

    PUT /api/v1/projects/:id/pull_requests/:number/merge.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current pull request.

### Input:

commit_message
: _Optional_ **string** the message that will be used for the merge commit

### Request:

<%= json(:pull_request_merge_request) %>

### Response:

<%= json(:pull_request_merge_response) %>

### Example:
<%= json(:pull_request_merge_response_example) %>

