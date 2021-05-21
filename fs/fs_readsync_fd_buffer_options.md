<!-- YAML
added:
 - v13.13.0
 - v12.17.0
changes:
  - version:
     - v13.13.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/32460
    description: Options object can be passed in
                 to make offset, length and position optional.
-->

* `fd` {integer}
* `buffer` {Buffer|TypedArray|DataView}
* `options` {Object}
  * `offset` {integer} **Default:** `0`
  * `length` {integer} **Default:** `buffer.byteLength`
  * `position` {integer|bigint} **Default:** `null`
* Returns: {number}

Returns the number of `bytesRead`.

Similar to the above `fs.readSync` function, this version takes an optional `options` object.
If no `options` object is specified, it will default with the above values.

For detailed information, see the documentation of the asynchronous version of
this API: [`fs.read()`][].

