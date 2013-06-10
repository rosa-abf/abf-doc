---
title: Product Build Lists | ABF API
---

# Product Build Lists API

* [Get a single product build list](#get-a-single-product-build-list)
* [List product build lists](#list-product-build-lists)
* [List product build lists for a product](#list-product-build-lists-for-a-product)
* [Create product build list](#create-product-build-list)
* [Destroy product build list](#destroy-product-build-list)
* [Update product build list](#update-product-build-list)
* [Cancel product build list](#cancel-product-build-list)

## Get a single product build list

Available statuses for product build list:
:   * `0`    — build complete;
    * `1`    — build failed;
    * `2`    — build pending;
    * `3`    — build started;
    * `4`    — build canceled;
    * `5`    — build canceling;

    GET /api/v1/product_build_lists/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_data_response) %>

### Example:

<%= json(:product_build_list_data_response_example) %>

## List product build lists

Look at [Product build list status](#get-a-single-product-build-list).

    GET /api/v1/product_build_lists.json

### Parameters:

page
: _Optional_ **Integer** - page number of product build lists results list.

per_page
: _Optional_ **Integer** - amount of product build list per one page. Default 20, maximum 100.

### Response:

<%= json(:product_build_list_response) %>

### Example of request url:

> /api/v1/product_build_lists.json

### Examples of responses:

<%= json(:product_build_list_response_example) %>

## List product build lists for a product

Look at [Product build list status](#get-a-single-product-build-list).

    GET /api/v1/products/:product_id/product_build_lists.json

### Parameters:

page
: _Optional_ **Integer** - page number of product build lists results list.

per_page
: _Optional_ **Integer** - amount of product build list per one page. Default 20, maximum 100.

### Response:

<%= json(:product_build_list_response) %>

### Example of request url:

> /api/v1/products/42/product_build_lists.json

### Examples of responses:

<%= json(:product_build_list_response_example) %>

## Create product build list

    POST /api/v1/product_build_list.json

### Input:

product_id
: _Required_ **Integer** identifier of product.

project_id
: _Optional_ **Integer** identifier of project.

commit_hash:
: _Required_ **String** SHA of project commit for which need to run assembly.

arch_id:
: _Required_ **integer** identifier architecture for which need to run assembly.

main_script:
: _Optional_ **String** main script.

params:
: _Optional_ **String** params for running script.

time_living:
: _Optional_ **Integer** Maximum time for building (between 2 and 720 minutes).

### Request:

<%= json(:product_build_list_create_request) %>

### Response:

<%= json(:product_build_list_create_response) %>

### Example:

<%= json(:product_build_list_create_response_example) %>

## Update product build list

By this request you can update product build list.
Only `not_delete` field can be updated and only if build has been completed.

    PUT /api/v1/product_build_lists/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Request:

<%= json(:product_build_list_update_request) %>

### Response:

<%= json(:product_build_list_update_response) %>

### Example:

<%= json(:product_build_list_update_response_example) %>

## Destroy product build list

By this request you can delete product build list.
Only product build list with status build completed (0), build failed (1) or build canceled (4) can be deleted.

    DELETE /api/v1/product_build_lists/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_destroy_response) %>

### Example:

<%= json(:product_build_list_destroy_response_example) %>

## Cancel product build list

By this request you can cancel product build list.
Only product build list with status build pending (2) or build started (3) can be canceled.

    PUT /api/v1/product_build_lists/:id/cancel.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_cancel_response) %>

### Example:

<%= json(:product_build_list_cancel_response_example) %>
