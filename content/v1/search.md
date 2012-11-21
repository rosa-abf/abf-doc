---
title: Search | ABF API
---

# Search API

* <a href="#search-around-the-abf">Search around the ABF</a>

## Search around the ABF

    GET /api/v1/search.json

### Input:

type:
: _Optional_ **String** type of search results (`projects`/`users`/`groups`/`platforms`).

query:
: _Optional_ **String** search term.

### Request

<%= json(:search_request) %>

### Request example:

<%= json(:search_request_example) %>

### Response:

<%= json(:search_response) %>

### Example:

<%= json(:search_response_example) %>