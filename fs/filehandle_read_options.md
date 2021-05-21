<!-- YAML
added:
 - v13.11.0
 - v12.17.0
-->
* `options` {Object}
  * `buffer` {Buffer|TypedArray|DataView} A buffer that will be filled with the
    file data read. **Default:** `Buffer.alloc(16384)`
  * `offset` {integer} The location in the buffer at which to start filling.
    **Default:** `0`
  * `length` {integer} The number of bytes to read. **Default:**
    `buffer.byteLength`
  * `position` {integer} The location where to begin reading data from the
    file. If `null`, data will be read from the current file position, and
    the position will be updated. If `position` is an integer, the current
    file position will remain unchanged. **Default:**: `null`
* Returns: {Promise} Fulfills upon success with an object with two properties:
  * `bytesRead` {integer} The number of bytes read
  * `buffer` {Buffer|TypedArray|DataView} A reference to the passed in `buffer`
    argument.

Reads data from the file and stores that in the given buffer.

If the file is not modified concurrently, the end-of-file is reached when the
number of bytes read is zero.

