
The `query` property is either the query string without the leading ASCII
question mark (`?`), or an object returned by the [`querystring`][] module's
`parse()` method. Whether the `query` property is a string or object is
determined by the `parseQueryString` argument passed to `url.parse()`.

For example: `'query=string'` or `{'query': 'string'}`

If returned as a string, no decoding of the query string is performed. If
returned as an object, both keys and values are decoded.

