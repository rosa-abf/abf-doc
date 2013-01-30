---
title: Products | ABF API
---

# Products API

* <a href="#get-a-single-product">Get a single product</a>
* <a href="#products-of-a-single-platform">List products of a single platform</a>
* <a href="#create-product">Create product</a>
* <a href="#update-a-single-product">Update a single product</a>
* <a href="#destroy-product">Destroy product</a>

## Get a single product

    GET /api/v1/products/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product.

### Response:

<%= json(:product_data_response) %>

### Example:

<%= json(:product_data_response_example) %>

## Products of a single platform

    GET /api/v1/platform/:id/products.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform.

### Response:

<%= json(:platform_products_response) %>

### Example:

<%= json(:platform_products_response_example) %>

## Create product

    POST /api/v1/products.json

### Input:

platform_id
: _Required_ **Integer** identifier of platform.

project_id
: _Required_ **Integer** identifier of project.

description:
: _Optional_ **String** product description.

name:
: _Required_ **String** product name.

main_script:
: _Optional_ **String** main script.

params:
: _Optional_ **String** params for running script.

time_living:
: _Optional_ **Integer** Maximum time for building (in minutes).

### Request:

<%= json(:product_create_request) %>

### Response:

<%= json(:product_create_response) %>

### Example:

<%= json(:product_create_response_example) %>

## Update a single product

    PUT /api/v1/products/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product.

### Input:

project_id
: _Required_ **Integer** identifier of project.

description:
: _Optional_ **String** product description.

name:
: _Required_ **String** product name.

main_script:
: _Optional_ **String** main script.

params:
: _Optional_ **String** params for running script.

time_living:
: _Optional_ **Integer** Maximum time for building (in minutes).

### Request:

<%= json(:product_update_request) %>

### Response:

<%= json(:product_update_response) %>

### Example:

<%= json(:product_update_response_example) %>

## Destroy product

    DELETE /api/v1/products/:id.json

### Parameters:

id
: _Required_ **Integer** identifier of current product.

### Response:

<%= json(:product_destroy_response) %>

### Example:

<%= json(:product_destroy_response_example) %>

