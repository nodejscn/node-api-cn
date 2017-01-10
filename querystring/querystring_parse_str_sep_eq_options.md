<!-- YAML
added: v0.1.25
-->

* `str` {String} The URL query string to parse
* `sep` {String} The substring used to delimit key and value pairs in the
  query string. Defaults to `'&'`.
* `eq` {String}. The substring used to delimit keys and values in the
  query string. Defaults to `'='`.
* `options` {Object}
  * `decodeURIComponent` {Function} The function to use when decoding
    percent-encoded characters in the query string. Defaults to
    `querystring.unescape()`.
  * `maxKeys` {number} Specifies the maximum number of keys to parse.
    Defaults to `1000`. Specify `0` to remove key counting limitations.

The `querystring.parse()` method parses a URL query string (`str`) into a
collection of key and value pairs.

For example, the query string `'foo=bar&abc=xyz&abc=123'` is parsed into:

```js
{
  foo: 'bar',
  abc: ['xyz', '123']
}
```

*Note*: The object returned by the `querystring.parse()` method _does not_
prototypically extend from the JavaScript `Object`. This means that the
typical `Object` methods such as `obj.toString()`, `obj.hasOwnProperty()`,
and others are not defined and *will not work*.

By default, percent-encoded characters within the query string will be assumed
to use UTF-8 encoding. If an alternative character encoding is used, then an
alternative `decodeURIComponent` option will need to be specified as illustrated
in the following example:

```js
// Assuming gbkDecodeURIComponent function already exists...

querystring.parse('w=%D6%D0%CE%C4&foo=bar', null, null,
  { decodeURIComponent: gbkDecodeURIComponent })
```

