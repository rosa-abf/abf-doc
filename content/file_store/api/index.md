---
title: RosaLab File Store API
---

# RosaLab File Store API

This describes the resources that make up the official Rosa File Store API. If you have any problems or requests please contact support.

**Note: This API is in a beta state. Breaking changes may occur.**

All of the urls in this manual have the same tail: .json. Because the default

* <a href="#schema">Schema</a>
* <a href="#client-errors">Client Errors</a>
* <a href="#http-verbs">HTTP Verbs</a>
* <a href="#authentication">Authentication</a>
* <a href="#rate-limiting">Rate Limiting</a>

## Schema

All API access is over HTTPS and all data is
sent and received as JSON.

<pre class="terminal">
$ curl -i https://file-store.rosalinux.ru/api/v1

HTTP/1.1 302 Found
Server: nginx/1.0.12
Date: Mon, 20 Feb 2012 11:15:49 GMT
Content-Type: text/html;charset=utf-8
Connection: keep-alive
Status: 302 Found
X-RateLimit-Limit: 2000
Location: http://file-store.rosalinux.ru
X-RateLimit-Remaining: 499
Content-Length: 0

</pre>

Blank fields are included as `null` instead of being omitted.

All timestamps are returned in unixtime format:

    1346762587

## Client Errors

There are three possible types of client errors on API calls that
receive request bodies.

Request without authorization will return error message:

<%= json(:error_auth) %>
<br/>

But if you set wrong pass or email you will receive this:

<%= json(:error_wrong_pass) %>
<br/>

Rate limit exceed will return this:

<%= json(:error_rate_limit) %>
<br/>

Some requests can cause cancer of 404, 500 and 503 errors. In these situatins you will receive such data:

<%= json(:error_404) %>

&nbsp;

<%= json(:error_500) %>

&nbsp;

<%= json(:error_503) %>

If you don't have enough rights for requested action, you will receive
error response such this:

<%= json(:error_403) %>

and http status code will be 403.

## HTTP Verbs

Where possible, API v1 strives to use appropriate HTTP verbs for each
action.

GET
: Used for retrieving resources.

POST
: Used for creating resources, or performing custom actions (such as
merging a pull request).

PUT
: Used for replacing resources or collections. For PUT requests
with no `body` attribute, be sure to set the `Content-Length` header to zero.

DELETE
: Used for deleting resources.

## Authentication

We use *http auth basic* for authentification:

<pre class="terminal">
$ curl --user myuser@gmail.com:mypass -i https://file-store.rosalinux.ru/api/v1
</pre>

## Rate Limiting

We limit requests to API v1 to 2000 per hour. This is keyed off either your
login, your OAuth token, or request IP.  You can check the returned HTTP
headers of any API request to see your current status:

<pre class="terminal">
$ curl -i https://file-store.rosalinux.ru/whatever

HTTP/1.1 200 OK
Status: 200 OK
X-RateLimit-Limit: 2000
X-RateLimit-Remaining: 496
</pre>