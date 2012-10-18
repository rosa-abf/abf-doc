---
title: Groups | ABF API
---

# Groups API

* <a href="#list-advisories">List advisories</a>
* <a href="#get-a-single-advisory">Get a single advisory</a>

## List advisories

    GET /api/v1/advisories.json

### Response:

<%= json(:advisory_list_response) %>

### Example:

<%= json(:advisory_list_response_example) %>

## Get a single advisory

    GET /api/v1/advisories/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current advisory.

### Response:

<%= json(:advisory_data_response) %>

### Example:

<%= json(:advisory_data_response_example) %>