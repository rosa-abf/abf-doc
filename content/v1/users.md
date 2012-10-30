---
title: Users | ABF API
---

# Users API

* <a href="#get-a-single-user">Get a single user</a>
* <a href="#get-a-current-user">Get a current user</a>
* <a href="#update-a-current-user">Update a current user</a>
* <a href="#get-a-notification-settings-of-a-current-user">Get a notification settings of a current user</a>
* <a href="#update-a-notification-settings-for-a-current-user">Update a notification settings for a current user</a>

## Get a single user

    GET /api/v1/users/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of user.

### Response:

<%= json(:user_data_response) %>

### Example:

<%= json(:user_data_response_example) %>

## Get a current user

    GET /api/v1/user.json

### Response:

<%= json(:user_data_response) %>

### Example:

<%= json(:user_data_response_example) %>

## Update a current user

    PUT /api/v1/user.json

### Input:

name:
: _Optional_ **String** user name.

email:
: _Optional_ **String** user email.

language:
: _Optional_ **String** user language (`ru` or `en`).

professional_experience:
: _Optional_ **String** user professional experience.

site:
: _Optional_ **String** user site.

company:
: _Optional_ **String** user company.

location:
: _Optional_ **String** user location.

### Request:

<%= json(:user_update_request) %>

### Response:

<%= json(:user_update_response) %>

### Example:

<%= json(:user_update_response_example) %>

## Get a notification settings of a current user

    GET /api/v1/user/notifiers.json

### Response:

<%= json(:user_notifiers_response) %>

### Example:

<%= json(:user_notifiers_response_example) %>

## Update a notification settings for a current user

    PUT /api/v1/user/notifiers.json

### Input:

can_notify:
: _Optional_ **Boolean** notifications by email.

new_comment_commit_owner:
: _Optional_ **Boolean** notify about comments to my commit.

new_comment_commit_repo_owner:
: _Optional_ **Boolean** notify about comments to my repository commits.

new_comment_commit_commentor:
: _Optional_ **Boolean** notify about comments after my commit.

new_comment:
: _Optional_ **Boolean** new task comment notifications.

new_comment_reply:
: _Optional_ **Boolean** new reply of comment notifications.

new_issue:
: _Optional_ **Boolean** new task notifications.

issue_assign:
: _Optional_ **Boolean** new task assignment notifications.

new_build:
: _Optional_ **Boolean** notify about my build tasks.

new_associated_build:
: _Optional_ **Boolean** notify about associated with me build tasks.

### Request:

<%= json(:user_update_notifiers_request) %>

### Response:

<%= json(:user_update_notifiers_response) %>

### Example:

<%= json(:user_update_notifiers_response_example) %>
