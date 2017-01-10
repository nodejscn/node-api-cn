<!-- YAML
added: v0.11.2
-->

* `path` {String}
* Returns: {Boolean}

The `path.isAbsolute()` method determines if `path` is an absolute path.

If the given `path` is a zero-length string, `false` will be returned.

For example on POSIX:

```js
path.isAbsolute('/foo/bar') // true
path.isAbsolute('/baz/..')  // true
path.isAbsolute('qux/')     // false
path.isAbsolute('.')        // false
```

On Windows:

```js
path.isAbsolute('//server')    // true
path.isAbsolute('\\\\server')  // true
path.isAbsolute('C:/foo/..')   // true
path.isAbsolute('C:\\foo\\..') // true
path.isAbsolute('bar\\baz')    // false
path.isAbsolute('bar/baz')     // false
path.isAbsolute('.')           // false
```

A [`TypeError`][] is thrown if `path` is not a string.

