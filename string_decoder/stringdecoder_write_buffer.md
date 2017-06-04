<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: Each invalid character is now replaced by a single replacement
                 character instead of one for each individual byte.
-->

* `buffer` {Buffer} 一个包含了要解码的字节的 `Buffer`。

返回一个解码后的字符串，并确保 `Buffer` 末尾的任何不完整的多字节字符从返回的字符串中被过滤并保存在一个内部的 buffer 中用于下次调用 `stringDecoder.write()` 或 `stringDecoder.end()`。

