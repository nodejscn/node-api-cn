<!-- YAML
added: v10.0.0
-->

* `filehandle` {FileHandle}
* `buffer` {Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* Returns: {Promise}

Write `buffer` to the file specified by `filehandle`.

The `Promise` is resolved with an object containing a `bytesWritten` property
identifying the number of bytes written, and a `buffer` property containing
a reference to the `buffer` written.

`offset` determines the part of the buffer to be written, and `length` is
an integer specifying the number of bytes to write.

`position` refers to the offset from the beginning of the file where this data
should be written. If `typeof position !== 'number'`, the data will be written
at the current position. See pwrite(2).

It is unsafe to use `fsPromises.write()` multiple times on the same file
without waiting for the `Promise` to be resolved (or rejected). For this
scenario, `fs.createWriteStream` is strongly recommended.

On Linux, positional writes do not work when the file is opened in append mode.
The kernel ignores the position argument and always appends the data to
the end of the file.

