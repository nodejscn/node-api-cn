<!-- YAML
added: v0.7.9
-->

* {String}

Provides the platform-specific path segment separator:

* `\` on Windows
* `/` on POSIX

For example on POSIX:

```js
'foo/bar/baz'.split(path.sep)
// Returns: ['foo', 'bar', 'baz']
```

On Windows:

```js
'foo\\bar\\baz'.split(path.sep)
// Returns: ['foo', 'bar', 'baz']
```

