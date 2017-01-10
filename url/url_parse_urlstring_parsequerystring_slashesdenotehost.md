<!-- YAML
added: v0.1.25
-->

* `urlString` {String} The URL string to parse.
* `parseQueryString` {Boolean} If `true`, the `query` property will always
  be set to an object returned by the [`querystring`][] module's `parse()`
  method. If `false`, the `query` property on the returned URL object will be an
  unparsed, undecoded string. Defaults to `false`.
* `slashesDenoteHost` {Boolean} If `true`, the first token after the literal
  string `//` and preceding the next `/` will be interpreted as the `host`.
  For instance, given `//foo/bar`, the result would be
  `{host: 'foo', pathname: '/bar'}` rather than `{pathname: '//foo/bar'}`.
  Defaults to `false`.

The `url.parse()` method takes a URL string, parses it, and returns a URL
object.

