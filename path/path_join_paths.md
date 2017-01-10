<!-- YAML
added: v0.1.16
-->

* `...paths` {String} A sequence of path segments
* Returns: {String}

The `path.join()` method joins all given `path` segments together using the
platform specific separator as a delimiter, then normalizes the resulting path.

Zero-length `path` segments are ignored. If the joined path string is a
zero-length string then `'.'` will be returned, representing the current
working directory.

For example:

```js
path.join('/foo', 'bar', 'baz/asdf', 'quux', '..')
// Returns: '/foo/bar/baz/asdf'

path.join('foo', {}, 'bar')
// throws TypeError: Arguments to path.join must be strings
```

A [`TypeError`][] is thrown if any of the path segments is not a string.

