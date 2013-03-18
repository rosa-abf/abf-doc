---
title: Maintainers | ABF API
---

# Maintainers API

* <a href="#list-maintainers">List maintainers</a>

## List maintainers
  Parameter "url" in block "Package" is available only for new core.

    GET /api/v1/platforms/:id/maintainers.json

### Parameters:

id
: _Required_ **Integer** identifier of current platform

package_name
: _Optional_ **string** — package name. You can use this parameters for searching data about specific package or group of packages.

### Request examples:

    /api/v1/platforms/64/maintainers.json

    /api/v1/platforms/64/maintainers.json?package_name=alpine

### Response:

<%= json(:maintainer_list_response) %>

### Example:

<%= json(:maintainer_list_response_example) %>
