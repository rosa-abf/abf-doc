---
title: Product Build Lists | ABF API
---

просмотр списка сборочных листов продукта;

# Product Build Lists API

* <a href="#get-a-single-product-build-list">Get a single product build list</a>
* <a href="#create-product-build-list">Create product build list</a>
* <a href="#destroy-product-build-list">Destroy product build list</a>
* <a href="#cancel-product-build-list">Cancel product build list</a>

## Get a single product build list

    GET /api/v1/product_build_lists/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_data_response) %>

### Example:

<%= json(:product_build_list_data_response_example) %>

## Create product build list

    POST /api/v1/product_build_list.json

### Input:

product_id
: _Required_ **Integer** identifier of product.

project_id
: _Optional_ **Integer** identifier of project.

project_version:
: _Required_ **String** branch or tag name.

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

## Destroy product build list

    DELETE /api/v1/product_build_lists/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_destroy_response) %>

### Example:

<%= json(:product_build_list_destroy_response_example) %>

## Cancel product build list

    PUT /api/v1/product_build_lists/:id/cancel.json

### Parameters:

id
: _Required_ **Integer** identifier of current product build list.

### Response:

<%= json(:product_build_list_cancel_response) %>

### Example:

<%= json(:product_build_list_cancel_response_example) %>
