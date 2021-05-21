<!-- YAML
added:
 - v13.11.0
 - v12.17.0
changes:
  - version:
     - v13.11.0
     - v12.17.0
    pr-url: https://github.com/nodejs/node/pull/31402
    description: Options object can be passed in
                 to make Buffer, offset, length and position optional.
-->
* `fd` {integer}
* `options` {Object}
  * `buffer` {Buffer|TypedArray|DataView} **Default:** `Buffer.alloc(16384)`
  * `offset` {integer} **Default:** `0`
  * `length` {integer} **Default:** `buffer.byteLength`
  * `position` {integer|bigint} **Default:** `null`
* `callback` {Function}
  * `err` {Error}
  * `bytesRead` {integer}
  * `buffer` {Buffer}

Similar to the [`fs.read()`][] function, this version takes an optional
`options` object. If no `options` object is specified, it will default with the
above values.

