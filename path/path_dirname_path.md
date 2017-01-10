<!-- YAML
added: v0.1.16
-->

* `path` {String}
* Returns: {String}

The `path.dirname()` method returns the directory name of a `path`, similar to
the Unix `dirname` command.

For example:

```js
path.dirname('/foo/bar/baz/asdf/quux')
// Returns: '/foo/bar/baz/asdf'
```

A [`TypeError`][] is thrown if `path` is not a string.

