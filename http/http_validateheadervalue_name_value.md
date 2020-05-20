<!-- YAML
added: v14.3.0
-->

* `name` {string}
* `value` {any}

Performs the low-level validations on the provided `value` that are done when
`res.setHeader(name, value)` is called.

Passing illegal value as `value` will result in a [`TypeError`][] being thrown.
* Undefined value error is identified by `code: 'ERR_HTTP_INVALID_HEADER_VALUE'`.
* Invalid value character error is identified by `code: 'ERR_INVALID_CHAR'`.

It is not necessary to use this method before passing headers to an HTTP request
or response. The HTTP module will automatically validate such headers.

Examples:

```js
const { validateHeaderValue } = require('http');

try {
  validateHeaderValue('x-my-header', undefined);
} catch (err) {
  err instanceof TypeError; // --> true
  err.code === 'ERR_HTTP_INVALID_HEADER_VALUE'; // --> true
  err.message; // --> 'Invalid value "undefined" for header "x-my-header"'
}

try {
  validateHeaderValue('x-my-header', 'oʊmɪɡə');
} catch (err) {
  err instanceof TypeError; // --> true
  err.code === 'ERR_INVALID_CHAR'; // --> true
  err.message; // --> 'Invalid character in header content ["x-my-header"]'
}
```



































































