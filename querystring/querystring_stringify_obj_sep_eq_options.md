<!-- YAML
added: v0.1.25
-->

* `obj` {Object} The object to serialize into a URL query string
* `sep` {String} The substring used to delimit key and value pairs in the
  query string. Defaults to `'&'`.
* `eq` {String}. The substring used to delimit keys and values in the
  query string. Defaults to `'='`.
* `options`
  * `encodeURIComponent` {Function} The function to use when converting
    URL-unsafe characters to percent-encoding in the query string. Defaults to
    `querystring.escape()`.

The `querystring.stringify()` method produces a URL query string from a
given `obj` by iterating through the object's "own properties".

For example:

```js
querystring.stringify({ foo: 'bar', baz: ['qux', 'quux'], corge: '' })
// returns 'foo=bar&baz=qux&baz=quux&corge='

querystring.stringify({foo: 'bar', baz: 'qux'}, ';', ':')
// returns 'foo:bar;baz:qux'
```

By default, characters requiring percent-encoding within the query string will
be encoded as UTF-8. If an alternative encoding is required, then an alternative
`encodeURIComponent` option will need to be specified as illustrated in the
following example:

```js
// Assuming gbkEncodeURIComponent function already exists,

querystring.stringify({ w: '中文', foo: 'bar' }, null, null,
  { encodeURIComponent: gbkEncodeURIComponent })
```

