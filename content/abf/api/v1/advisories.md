---
title: Advisories | ABF API
---

# Advisories API

* [List advisories](#list-advisories)
* [Get a single advisory](#get-a-single-advisory)
* [Create advisory](#create-advisory)
* [Attach to advisory](#attach-to-advisory)

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

## Create advisory

    POST /api/v1/advisories.json

### Input:

build_list_id:
: _Required_ **Integer** identifier of build list.

description:
: _Required_ **String** advisory description.

references:
: _Optional_ **String** advisory references.

### Request:

<%= json(:advisory_create_request) %>

### Response:

<%= json(:advisory_create_response) %>

### Examples:

<%= json(:advisory_create_response_example) %>

## Attach to advisory

    PUT /api/v1/advisories/:id.json

### Parameters:
id
: _Integer_ identifier of current advisory

### Input:

build_list_id:
: _Required_ **Integer** identifier of build list.

### Request:

<%= json(:advisory_attach_request) %>

### Response:

<%= json(:advisory_attach_response) %>

### Examples:

<%= json(:advisory_attach_response_example) %>