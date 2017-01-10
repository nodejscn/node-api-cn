<!-- YAML
added: v0.5.0
-->

* `from` {String}
* `to` {String}
* Returns: {String}

The `path.relative()` method returns the relative path from `from` to `to`.
If `from` and `to` each resolve to the same path (after calling `path.resolve()`
on each), a zero-length string is returned.

If a zero-length string is passed as `from` or `to`, the current working
directory will be used instead of the zero-length strings.

For example on POSIX:

```js
path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb')
// Returns: '../../impl/bbb'
```

On Windows:

```js
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb')
// Returns: '..\\..\\impl\\bbb'
```

A [`TypeError`][] is thrown if neither `from` nor `to` is a string.

