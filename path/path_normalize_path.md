<!-- YAML
added: v0.1.23
-->

* `path` {String}
* Returns: {String}

The `path.normalize()` method normalizes the given `path`, resolving `'..'` and
`'.'` segments.

When multiple, sequential path segment separation characters are found (e.g.
`/` on POSIX and `\` on Windows), they are replaced by a single instance of the
platform specific path segment separator. Trailing separators are preserved.

If the `path` is a zero-length string, `'.'` is returned, representing the
current working directory.

For example on POSIX:

```js
path.normalize('/foo/bar//baz/asdf/quux/..')
// Returns: '/foo/bar/baz/asdf'
```

On Windows:

```js
path.normalize('C:\\temp\\\\foo\\bar\\..\\');
// Returns: 'C:\\temp\\foo\\'
```

A [`TypeError`][] is thrown if `path` is not a string.

