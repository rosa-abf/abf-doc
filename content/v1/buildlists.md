---
title: Build lists | ABF API
---

# Build lists API

* <a href="#get-a-single-build-list">Get a single build list</a>
* <a href="#create-build-list">Create build list</a>
* <a href="#cancel-build-list">Cancel build list</a>
* <a href="#publish-build-list">Publish build list</a>
* <a href="#create-container">Create container</a>
* <a href="#reject-publish-build-list">Reject publish build list</a>
* <a href="#list-build-lists">List build lists</a>
* <a href="#list-build-lists-for-a-project">List build lists for a project</a>
* <a href="#destroy-build-list">Destroy build list</a>

## Get a single build list
  Block "Logs" is available only for new core.<br/>
  The value of parameter "url" in block "Packages" is empty for old core.

    GET /api/v1/build_lists/:id.json

### Available statuses for parameter "container_status":
* `4000` — waiting for request for publishing container;
* `6000` — container has been published;
* `7000` — container is being published;
* `8000` — publishing error.

### Parameters:
id
: _Integer_ identifier of current build list

### Response:

<%= json(:build_list_show_parameters) %>

### Example:

<%= json(:build_list_show_example) %>

## Create build list

Create new build list for project.

    POST /api/v1/build_lists.json

### Input:

project_id
: _Required_ **integer** — Identifier project for which need to run assembly.

commit_hash
: _Required_ **string** — SHA of project commit for which need to run assembly.

update_type
: _Required_ **string** — Informing customers about the priority and character of updates: `security`, `bugfix`, `enhancement`,`recommended` or `newpackage`.

save_to_repository_id
: _Required_ **integer** — Repository identifier for package storage. List of repositories can be find in api call:
<a href="/v1/projects/#get-a-single-project">see repositories section.</a>

build_for_platform_id
: _Required_ **integer** — Identifier of platform for which need to run assembly. List of platforms can be find in api call:
<a href="/v1/platforms/#list-of-platforms-for-which-you-can-create-build-list">list of platforms.</a>

auto_publish
: _Required_ **boolean** — `true` to enable automatic publiction build list if the build succeeds, `false` allow manually publication. If in repository for package storage disabled publication without QA, parameter auto_publish automatically will be set to false.

include_repos
: _Required_ **array** of **integers** — Repositories to connect for building this build list. Repositories must belong to platform(build_for_platform_id) for which performed assembly.

arch_id
: _Required_ **integer** — Identifier architecture for which need to run assembly.

use_save_to_repository
: _Optional_ **boolean** Use repository for package storage on building. Only for personal platforms. Default value: `true`.

### Request

<%= json(:build_list_create_parameters) %>

### Request example:

<%= json(:build_list_create_example) %>

### Response:

<%= json(:build_list_create_response) %>

### Response example:

<%= json(:build_list_create_response_example) %>

## Cancel build list

By this request you can cancel build list.
Only build list with status build pending (2000) or build started (3000) can be canceled.

    PUT /api/v1/build_lists/:id/cancel.json

### Parameters:
id
: _Integer_ identifier of current build list

### Response:

<%= json(:build_list_cancel_response) %>

### Example:

<%= json(:build_list_cancel_response_example) %>

&nbsp;

<%= json(:build_list_cancel_response_example2) %>

## Publish build list

By this request you can publish build list.
Only build list with status build complete (0), publishing error (8000) or tests failed (11000) can be published.<br/>
Admin of platform/repository has access to publish build list again with status published (6000).<br/>
Be careful: secondary publication will be able to break relationships in the repository!

    PUT /api/v1/build_lists/:id/publish.json

### Parameters:
id
: _Integer_ identifier of current build list

### Response:

<%= json(:build_list_publish_response) %>

### Example:

<%= json(:build_list_publish_response_example) %>

&nbsp;

<%= json(:build_list_publish_response_example2) %>

## Create container

By this request you can create container.
Container can be created only for build list with statuses build complete (0) and tests failed (11000).

    PUT /api/v1/build_lists/:id/create_container.json

### Parameters:
id
: _Integer_ identifier of current build list

### Response:

<%= json(:build_list_create_container_response) %>

### Example:

<%= json(:build_list_create_container_response_example) %>

&nbsp;

<%= json(:build_list_create_container_response_example2) %>

## Reject publish build list

By this request you can reject publish build list.
Only build list with status build complete (0) or publishing error (8000) and saved to repository with turn on QA check can be rejected.

    PUT /api/v1/build_lists/:id/reject_publish.json

### Parameters:
id
: _Integer_ identifier of current build list

### Response:

<%= json(:build_list_reject_response) %>

### Example:

<%= json(:build_list_reject_response_example) %>

&nbsp;

<%= json(:build_list_reject_response_example2) %>

## List build lists

By this way you can search build list you need.

    GET /api/v1/build_lists.json?<search params>

### Parameters:

page
: _Optional_ **Integer** - page number of build lists results list.

per_page
: _Optional_ **Integer** - amount of build list per one page. Default 20, maximum 100.

filter[status]
: _Optional_ **integer** - code of the build status
:   * `0`     — build complete;
    * `1`     — platform not found;
    * `2`     — platform pending;
    * `3`     — project not found;
    * `4`     — project version not found;
    * `666`   — build error;
    * `2000`  — build pending;
    * `3000`  — build started;
    * `4000`  — waiting for response;
    * `5000`  — build canceled;
    * `6000`  — build has been published;
    * `7000`  — build is being published;
    * `8000`  — publishing error;
    * `9000`  — publishing rejected;
    * `10000` — build is canceling;
    * `11000` — tests failed.

filter[arch_id]
: _Optional_ **integer** - identifier of the architecture.

filter[is_circle]
: _Optional_ **boolean** - recurrent build (true or false). Default: `false`

filter[project_name]
: _Optional_ **string** — project name.

filter[updated_at_start / updated_at_end]
: _Optional_ **unixtime** - start and end of the build list last change date diapason.

filter[ownership]
: _Optional_ `owned`, `related` or `index` - ownership type. Default: `owned`.

filter[mass_build_id]
: _Optional_ **integer** — mass build identifier.

filter[save_to_platform_id]
: _Optional_ **integer** - platform id for build save.

### Response:

<%= json(:build_list_search_response) %>

### Example of request url:

> /api/v1/build_lists.json?filter[project_name]=rails

> /api/v1/build_lists.json?filter[ownership]=owned&filter[status]=6000&filter[arch_id]=2

### Examples of responses:

<%= json(:build_list_search_response_example) %>

## List build lists for a project

    GET /api/v1/projects/:project_id/build_lists.json?<search params>

### Parameters:

Look at <a href="#list-build-lists">List build lists</a>

### Response:

<%= json(:build_list_search_response) %>

### Example of request url:

> /api/v1/projects/42/build_lists.json?filter[status]=6000

### Examples of responses:

<%= json(:build_list_search_response_example) %>


## Destroy build list

You can't destroy build list. Only cancel it. :)

