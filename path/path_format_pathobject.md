<!-- YAML
added: v0.11.15
-->

* `pathObject` {Object}
  * `dir` {String}
  * `root` {String}
  * `base` {String}
  * `name` {String}
  * `ext` {String}
* Returns: {String}

The `path.format()` method returns a path string from an object. This is the
opposite of [`path.parse()`][].

The following process is used when constructing the path string:

* `output` is set to an empty string.
* If `pathObject.dir` is specified, `pathObject.dir` is appended to `output`
  followed by the value of `path.sep`;
* Otherwise, if `pathObject.root` is specified, `pathObject.root` is appended
  to `output`.
* If `pathObject.base` is specified, `pathObject.base` is appended to `output`;
* Otherwise:
  * If `pathObject.name` is specified, `pathObject.name` is appended to `output`
  * If `pathObject.ext` is specified, `pathObject.ext` is appended to `output`.
* Return `output`

For example, on POSIX:

```js
// If `dir` and `base` are provided,
// `${dir}${path.sep}${base}`
// will be returned.
path.format({
  dir: '/home/user/dir',
  base: 'file.txt'
});
// Returns: '/home/user/dir/file.txt'

// `root` will be used if `dir` is not specified.
// If only `root` is provided or `dir` is equal to `root` then the
// platform separator will not be included.
path.format({
  root: '/',
  base: 'file.txt'
});
// Returns: '/file.txt'

// `name` + `ext` will be used if `base` is not specified.
path.format({
  root: '/',
  name: 'file',
  ext: '.txt'
});
// Returns: '/file.txt'

// `base` will be returned if `dir` or `root` are not provided.
path.format({
  base: 'file.txt'
});
// Returns: 'file.txt'
```

On Windows:

```js
path.format({
    root : "C:\\",
    dir : "C:\\path\\dir",
    base : "file.txt",
    ext : ".txt",
    name : "file"
});
// Returns: 'C:\\path\\dir\\file.txt'
```

