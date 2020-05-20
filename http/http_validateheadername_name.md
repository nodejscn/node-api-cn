<!-- YAML
added: v14.3.0
-->

* `name` {string}

Performs the low-level validations on the provided `name` that are done when
`res.setHeader(name, value)` is called.

Passing illegal value as `name` will result in a [`TypeError`][] being thrown,
identified by `code: 'ERR_INVALID_HTTP_TOKEN'`.

It is not necessary to use this method before passing headers to an HTTP request
or response. The HTTP module will automatically validate such headers.
Examples:

Example:
```js
const { validateHeaderName } = require('http');

try {
  validateHeaderName('');
} catch (err) {
  err instanceof TypeError; // --> true
  err.code; // --> 'ERR_INVALID_HTTP_TOKEN'
  err.message; // --> 'Header name must be a valid HTTP token [""]'
}
```

