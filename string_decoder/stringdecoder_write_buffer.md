<!-- YAML
added: v0.1.99
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9618
    description: Each invalid character is now replaced by a single replacement
                 character instead of one for each individual byte.
-->

* `buffer` {Buffer} 包含待解码字节的 `Buffer`。

返回一个解码后的字符串，并确保返回的字符串不包含 `Buffer` 末尾残缺的多字节字符，残缺的多字节字符会被保存在一个内部的 buffer 中用于下次调用 `stringDecoder.write()` 或 `stringDecoder.end()`。

