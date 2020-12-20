
ES modules are resolved and cached as URLs. This means that files containing
special characters such as `#` and `?` need to be escaped.

`file:`, `node:`, and `data:` URL schemes are supported. A specifier like
`'https://example.com/app.js'` is not supported natively in Node.js unless using
a [custom HTTPS loader][].

