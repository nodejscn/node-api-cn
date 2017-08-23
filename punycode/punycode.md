<!-- YAML
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7941
    description: Accessing this module will now emit a deprecation warning.
-->

> Stability: 0 - Deprecated

**The version of the punycode module bundled in Node.js is being deprecated**.
In a future major version of Node.js this module will be removed. Users
currently depending on the `punycode` module should switch to using the
userland-provided [Punycode.js][] module instead.

The `punycode` module is a bundled version of the [Punycode.js][] module. It
can be accessed using:

```js
const punycode = require('punycode');
```

[Punycode][] is a character encoding scheme defined by RFC 3492 that is
primarily intended for use in Internationalized Domain Names. Because host
names in URLs are limited to ASCII characters only, Domain Names that contain
non-ASCII characters must be converted into ASCII using the Punycode scheme.
For instance, the Japanese character that translates into the English word,
`'example'` is `'例'`. The Internationalized Domain Name, `'例.com'` (equivalent
to `'example.com'`) is represented by Punycode as the ASCII string
`'xn--fsq.com'`.

The `punycode` module provides a simple implementation of the Punycode standard.

*Note*: The `punycode` module is a third-party dependency used by Node.js and
made available to developers as a convenience. Fixes or other modifications to
the module must be directed to the [Punycode.js][] project.

