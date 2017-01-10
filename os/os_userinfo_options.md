<!-- YAML
added: v6.0.0
-->

* `options` {Object}
  * `encoding` {String} Character encoding used to interpret resulting strings.
    If `encoding` is set to `'buffer'`, the `username`, `shell`, and `homedir`
    values will be `Buffer` instances. (Default: 'utf8')
* Returns: {Object}

The `os.userInfo()` method returns information about the currently effective
user -- on POSIX platforms, this is typically a subset of the password file. The
returned object includes the `username`, `uid`, `gid`, `shell`, and `homedir`.
On Windows, the `uid` and `gid` fields are `-1`, and `shell` is `null`.

The value of `homedir` returned by `os.userInfo()` is provided by the operating
system. This differs from the result of `os.homedir()`, which queries several
environment variables for the home directory before falling back to the
operating system response.

