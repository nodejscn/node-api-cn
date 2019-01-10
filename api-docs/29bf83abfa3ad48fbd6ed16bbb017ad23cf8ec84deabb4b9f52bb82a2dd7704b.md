<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `atime` {number|string|Date}
* `mtime` {number|string|Date}
* Returns: {Promise}

Change the file system timestamps of the object referenced by `path` then
resolves the `Promise` with no arguments upon success.

The `atime` and `mtime` arguments follow these rules:
- Values can be either numbers representing Unix epoch time, `Date`s, or a
  numeric string like `'123456789.0'`.
- If the value can not be converted to a number, or is `NaN`, `Infinity` or
  `-Infinity`, an `Error` will be thrown.

