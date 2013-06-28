---
title: Issues | ABF API
---

# Issues API

* <a href="#list-issues">List issues</a>
* <a href="#list-issues-for-a-project">List issues for a project</a>
* <a href="#get-a-single-issue">Get a single issue</a>
* <a href="#create-an-issue">Create an issue</a>
* <a href="#update-a-single-issue">Update a single issue</a>

## List issues

List all issues across all the authenticated user’s projects including owned projects, member projects, and group projects:

    GET /api/v1/issues.json

List all issues across owned and member projects for the authenticated user:

    GET /api/v1/user/issues.json

List all issues for a given group for the authenticated user:

    GET /api/v1/group/:id/issues.json

### Parameters

filter
: _Optional_ **String**
: * `assigned`: Issues assigned to you (default)
  * `created`: Issues created by you
  * `all`: All issues the authenticated user can see

status
: _Optional_ **String** `open` (default), `closed`

labels
: _Optional_ **String** list of comma separated Label names.
Example: `Bug,Feature,Security`

sort
: _Optional_ **String** `submitted` (default), `updated`.

direction
: _Optional_ **String** `asc` or `desc` (default).

since
: _Optional_ **Integer** of a timestamp in Unix time format.

### Response:

<%= json(:issues_list_response) %>

### Example:

<%= json(:issues_list_response_example) %>

## List issues for a project

    GET /api/v1/projects/:id/issues.json

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

labels
: _Optional_ **String** list of comma separated Label names.
Example: `Bug,Feature,Security`

sort
: _Optional_ **String** `submitted` (default), `updated`.

direction
: _Optional_ **String** `asc` or `desc` (default).

since
: _Optional_ **Integer** of a timestamp in Unix time format.

### Response:

<%= json(:issues_list_response) %>

### Example:

<%= json(:issues_list_response_example) %>

## Get a single issue

    GET /api/v1/projects/:project_id/issues/:number.json

### Parameters:

project_id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current issue.

### Response:

<%= json(:issue_data_response) %>

### Example:

<%= json(:issue_data_response_example) %>

## Create an issue

Any authenticated user with read access to a project can create an issue.

    POST /api/v1/projects/:id/issues.json

### Input

title
: _Required_ **String**

body
: _Required_ **String**

assignee
: _Optional_ **Integer** - Id for the user that this issue should be
assigned to. _NOTE: Only users with push access can set the assignee for new
issues. The assignee is silently dropped otherwise._

labels
: _Optional_ **array** of **strings** - Labels to associate with this
issue. _NOTE: Only users with push access can set labels for new issues. Labels are
silently dropped otherwise._

### Request:

<%= json(:issue_create_request) %>

### Response:

<%= json(:issue_create_response) %>

### Examples:

<%= json(:issue_create_response_example) %>

## Update a single issue

    PUT /api/v1/projects/:id/issues/:number.json

### Parameters:

id
: _Required_ **Integer** identifier of current project.

number
: _Required_ **Integer** identifier of current issue.

### Input:

title
: _Optional_ **String**

body
: _Optional_ **String**

assignee
: _Optional_ **Integer** - Identifier for the user that this issue should be
assigned to.

status
: _Optional_ **String** - State of the issue: `open` or `closed`.

labels
: _Optional_ **Array** of **Strings** - Labels to associate with this
issue. Pass one or more Labels to _replace_ the set of Labels on this
Issue. Send an empty array (`[]`) to clear all Labels from the Issue.

### Request:

<%= json(:issue_update_request) %>

### Response:

<%= json(:issue_update_response) %>

### Example:

<%= json(:issue_update_response_example) %>

