<!-- YAML
added: v10.0.0
-->
* `buffer` {Buffer|Uint8Array}
* `offset` {integer}
* `length` {integer}
* `position` {integer}
* Returns: {Promise}

Read data from the file.

`buffer` is the buffer that the data will be written to.

`offset` is the offset in the buffer to start writing at.

`length` is an integer specifying the number of bytes to read.

`position` is an argument specifying where to begin reading from in the file.
If `position` is `null`, data will be read from the current file position,
and the file position will be updated.
If `position` is an integer, the file position will remain unchanged.

Following successful read, the `Promise` is resolved with an object with a
`bytesRead` property specifying the number of bytes read, and a `buffer`
property that is a reference to the passed in `buffer` argument.

