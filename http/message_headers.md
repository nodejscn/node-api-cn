<!-- YAML
added: v0.1.5
-->

* {Object}

The request/response headers object.

Key-value pairs of header names and values. Header names are lower-cased.
Example:

```js
// Prints something like:
//
// { 'user-agent': 'curl/7.22.0',
//   host: '127.0.0.1:8000',
//   accept: '*/*' }
console.log(request.headers);
```

Duplicates in raw headers are handled in the following ways, depending on the
header name:

* Duplicates of `age`, `authorization`, `content-length`, `content-type`,
`etag`, `expires`, `from`, `host`, `if-modified-since`, `if-unmodified-since`,
`last-modified`, `location`, `max-forwards`, `proxy-authorization`, `referer`,
`retry-after`, or `user-agent` are discarded.
* `set-cookie` is always an array. Duplicates are added to the array.
* For all other headers, the values are joined together with ', '.

