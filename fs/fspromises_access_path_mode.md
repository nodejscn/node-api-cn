<!-- YAML
added: v10.0.0
-->

* `path` {string|Buffer|URL}
* `mode` {integer} **Default:** `fs.constants.F_OK`
* Returns: {Promise}

Tests a user's permissions for the file or directory specified by `path`.
The `mode` argument is an optional integer that specifies the accessibility
checks to be performed. The following constants define the possible values of
`mode`. It is possible to create a mask consisting of the bitwise OR of two or
more values (e.g. `fs.constants.W_OK | fs.constants.R_OK`).

* `fs.constants.F_OK` - `path` is visible to the calling process. This is useful
for determining if a file exists, but says nothing about `rwx` permissions.
Default if no `mode` is specified.
* `fs.constants.R_OK` - `path` can be read by the calling process.
* `fs.constants.W_OK` - `path` can be written by the calling process.
* `fs.constants.X_OK` - `path` can be executed by the calling process. This has
no effect on Windows (will behave like `fs.constants.F_OK`).

If the accessibility check is successful, the `Promise` is resolved with no
value. If any of the accessibility checks fail, the `Promise` is rejected
with an `Error` object. The following example checks if the file
`/etc/passwd` can be read and written by the current process.

```js
fsPromises.access('/etc/passwd', fs.constants.R_OK | fs.constants.W_OK)
  .then(() => console.log('can access'))
  .catch(() => console.error('cannot access'));
```

Using `fsPromises.access()` to check for the accessibility of a file before
calling `fsPromises.open()` is not recommended. Doing so introduces a race
condition, since other processes may change the file's state between the two
calls. Instead, user code should open/read/write the file directly and handle
the error raised if the file is not accessible.

