---
title: Maintainers | ABF API
---

# Maintainers API

* <a href="#list-maintainers">List maintainers</a>

## List maintainers

    GET /api/v1/platforms/:id/maintainers.json

### Request examples:

    /api/v1/platforms/64/maintainers.json

### Response:

<%= json(:maintainer_list_response) %>

### Example:

<%= json(:maintainer_list_response_example) %>
