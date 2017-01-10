<!-- YAML
added: v0.1.25
-->

* `path` {String}
* `ext` {String} An optional file extension
* Returns: {String}

The `path.basename()` methods returns the last portion of a `path`, similar to
the Unix `basename` command.

For example:

```js
path.basename('/foo/bar/baz/asdf/quux.html')
// Returns: 'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html')
// Returns: 'quux'
```

A [`TypeError`][] is thrown if `path` is not a string or if `ext` is given
and is not a string.

