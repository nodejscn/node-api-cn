<!-- YAML
added: v0.3.0
-->

* `headers` {Object}

Adds HTTP trailers (headers but at the end of the message) to the message.

Trailers are **only** be emitted if the message is chunked encoded. If not,
the trailer will be silently discarded.

HTTP requires the  `Trailer` header to be sent to emit trailers,
with a list of header fields in its value, e.g.

```js
message.writeHead(200, { 'Content-Type': 'text/plain',
                         'Trailer': 'Content-MD5' });
message.write(fileData);
message.addTrailers({ 'Content-MD5': '7895bf4b8828b55ceaf47747b4bca667' });
message.end();
```

Attempting to set a header field name or value that contains invalid characters
will result in a `TypeError` being thrown.

