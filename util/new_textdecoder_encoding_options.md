
* `encoding` {string} Identifies the `encoding` that this `TextDecoder` instance
  supports. Defaults to `'utf-8'`.
* `options` {Object}
  * `fatal` {boolean} `true` if decoding failures are fatal. Defaults to
    `false`. This option is only supported when ICU is enabled (see
    [Internationalization][]).
  * `ignoreBOM` {boolean} When `true`, the `TextDecoder` will include the byte
     order mark in the decoded result. When `false`, the byte order mark will
     be removed from the output. This option is only used when `encoding` is
     `'utf-8'`, `'utf-16be'` or `'utf-16le'`. Defaults to `false`.

Creates an new `TextDecoder` instance. The `encoding` may specify one of the
supported encodings or an alias.

