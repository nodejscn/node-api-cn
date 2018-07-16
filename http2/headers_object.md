
Headers are represented as own-properties on JavaScript objects. The property
keys will be serialized to lower-case. Property values should be strings (if
they are not they will be coerced to strings) or an `Array` of strings (in order
to send more than one value per header field).

```js
const headers = {
  ':status': '200',
  'content-type': 'text-plain',
  'ABC': ['has', 'more', 'than', 'one', 'value']
};

stream.respond(headers);
```

Header objects passed to callback functions will have a `null` prototype. This
means that normal JavaScript object methods such as
`Object.prototype.toString()` and `Object.prototype.hasOwnProperty()` will
not work.

For incoming headers:
* The `:status` header is converted to `number`.
* Duplicates of `:status`, `:method`, `:authority`, `:scheme`, `:path`,
`age`, `authorization`, `access-control-allow-credentials`,
`access-control-max-age`, `access-control-request-method`, `content-encoding`,
`content-language`, `content-length`, `content-location`, `content-md5`,
`content-range`, `content-type`, `date`, `dnt`, `etag`, `expires`, `from`,
`if-match`, `if-modified-since`, `if-none-match`, `if-range`,
`if-unmodified-since`, `last-modified`, `location`, `max-forwards`,
`proxy-authorization`, `range`, `referer`,`retry-after`, `tk`,
`upgrade-insecure-requests`, `user-agent` or `x-content-type-options` are
discarded.
* `set-cookie` is a string if present once or an array in case duplicates
are present.
* `cookie`: the values are joined together with '; '.
* For all other headers, the values are joined together with ', '.

```js
const http2 = require('http2');
const server = http2.createServer();
server.on('stream', (stream, headers) => {
  console.log(headers[':path']);
  console.log(headers.ABC);
});
```

