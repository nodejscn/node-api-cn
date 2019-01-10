<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: Each invalid character is now replaced by a single replacement
                 character instead of one for each individual byte.
-->

* `buffer` {Buffer|TypedArray|DataView} 包含要解码的字节的 `Buffer`、`TypedArray` 或 `DataView`。
* 返回: {string}

返回一个已解码的字符串，确保在返回的字符串不包含 `Buffer`、`TypedArray` 或 `DataView` 末尾的任何不完整的多字节字符，并将其存储在内部缓冲区中，以便下次调用 `stringDecoder.write()` 或 `stringDecoder.end()`。

