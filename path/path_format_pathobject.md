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

When providing properties to the `pathObject` remember that there are
combinations where one property has priority over another:

* `pathObject.root` is ignored if `pathObject.dir` is provided
* `pathObject.ext` and `pathObject.name` are ignored if `pathObject.base` exists

For example, on POSIX:

```js
// If `dir`, `root` and `base` are provided,
// `${dir}${path.sep}${base}`
// will be returned. `root` is ignored.
path.format({
  root: '/ignored',
  dir: '/home/user/dir',
  base: 'file.txt'
});
// Returns: '/home/user/dir/file.txt'

// `root` will be used if `dir` is not specified.
// If only `root` is provided or `dir` is equal to `root` then the
// platform separator will not be included. `ext` will be ignored.
path.format({
  root: '/',
  base: 'file.txt',
  ext: 'ignored'
});
// Returns: '/file.txt'

// `name` + `ext` will be used if `base` is not specified.
path.format({
  root: '/',
  name: 'file',
  ext: '.txt'
});
// Returns: '/file.txt'
```

On Windows:

```js
path.format({
  dir : "C:\\path\\dir",
  base : "file.txt"
});
// Returns: 'C:\\path\\dir\\file.txt'
```

