<!-- YAML
added: v0.1.25
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22715
    description: The Legacy URL API is deprecated. Use the WHATWG URL API.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7234
    description: URLs with a `file:` scheme will now always use the correct
                 number of slashes regardless of `slashes` option. A falsy
                 `slashes` option with no protocol is now also respected at all
                 times.
-->

> Stability: 0 - Deprecated: Use the WHATWG URL API instead.

* `urlObject` {Object|string} A URL object (as returned by `url.parse()` or
  constructed otherwise). If a string, it is converted to an object by passing
  it to `url.parse()`.

The `url.format()` method returns a formatted URL string derived from
`urlObject`.

```js
url.format({
  protocol: 'https',
  hostname: 'example.com',
  pathname: '/some/path',
  query: {
    page: 1,
    format: 'json'
  }
});

// => 'https://example.com/some/path?page=1&format=json'
```

If `urlObject` is not an object or a string, `url.format()` will throw a
[`TypeError`][].

The formatting process operates as follows:

* A new empty string `result` is created.
* If `urlObject.protocol` is a string, it is appended as-is to `result`.
* Otherwise, if `urlObject.protocol` is not `undefined` and is not a string, an
  [`Error`][] is thrown.
* For all string values of `urlObject.protocol` that *do not end* with an ASCII
  colon (`:`) character, the literal string `:` will be appended to `result`.
* If either of the following conditions is true, then the literal string `//`
  will be appended to `result`:
  * `urlObject.slashes` property is true;
  * `urlObject.protocol` begins with `http`, `https`, `ftp`, `gopher`, or
    `file`;
* If the value of the `urlObject.auth` property is truthy, and either
  `urlObject.host` or `urlObject.hostname` are not `undefined`, the value of
  `urlObject.auth` will be coerced into a string and appended to `result`
   followed by the literal string `@`.
* If the `urlObject.host` property is `undefined` then:
  * If the `urlObject.hostname` is a string, it is appended to `result`.
  * Otherwise, if `urlObject.hostname` is not `undefined` and is not a string,
    an [`Error`][] is thrown.
  * If the `urlObject.port` property value is truthy, and `urlObject.hostname`
    is not `undefined`:
    * The literal string `:` is appended to `result`, and
    * The value of `urlObject.port` is coerced to a string and appended to
      `result`.
* Otherwise, if the `urlObject.host` property value is truthy, the value of
  `urlObject.host` is coerced to a string and appended to `result`.
* If the `urlObject.pathname` property is a string that is not an empty string:
  * If the `urlObject.pathname` *does not start* with an ASCII forward slash
    (`/`), then the literal string `'/'` is appended to `result`.
  * The value of `urlObject.pathname` is appended to `result`.
* Otherwise, if `urlObject.pathname` is not `undefined` and is not a string, an
  [`Error`][] is thrown.
* If the `urlObject.search` property is `undefined` and if the `urlObject.query`
  property is an `Object`, the literal string `?` is appended to `result`
  followed by the output of calling the [`querystring`][] module's `stringify()`
  method passing the value of `urlObject.query`.
* Otherwise, if `urlObject.search` is a string:
  * If the value of `urlObject.search` *does not start* with the ASCII question
    mark (`?`) character, the literal string `?` is appended to `result`.
  * The value of `urlObject.search` is appended to `result`.
* Otherwise, if `urlObject.search` is not `undefined` and is not a string, an
  [`Error`][] is thrown.
* If the `urlObject.hash` property is a string:
  * If the value of `urlObject.hash` *does not start* with the ASCII hash (`#`)
    character, the literal string `#` is appended to `result`.
  * The value of `urlObject.hash` is appended to `result`.
* Otherwise, if the `urlObject.hash` property is not `undefined` and is not a
  string, an [`Error`][] is thrown.
* `result` is returned.

