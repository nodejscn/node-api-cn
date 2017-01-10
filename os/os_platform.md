<!-- YAML
added: v0.5.0
-->

* Returns: {String}

The `os.platform()` method returns a string identifying the operating system
platform as set during compile time of Node.js.

Currently possible values are:

* `'aix'`
* `'darwin'`
* `'freebsd'`
* `'linux'`
* `'openbsd'`
* `'sunos'`
* `'win32'`

Equivalent to [`process.platform`][].

*Note*: The value `'android'` may also be returned if the Node.js is built on
the Android operating system. However, Android support in Node.js is considered
to be experimental at this time.

