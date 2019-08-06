<!-- YAML
changes:
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/22861
    description: Runtime deprecation (for `digest === null`).
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11305
    description: End-of-Life (for `digest === undefined`).
  - version: v6.12.0
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/4047
    description: Runtime deprecation (for `digest === undefined`).
-->

Type: Runtime

Use of the [`crypto.pbkdf2()`][] API without specifying a digest was deprecated
in Node.js 6.0 because the method defaulted to using the non-recommended
`'SHA1'` digest. Previously, a deprecation warning was printed. Starting in
Node.js 8.0.0, calling `crypto.pbkdf2()` or `crypto.pbkdf2Sync()` with
`digest` set to `undefined` will throw a `TypeError`.

Beginning in Node.js v11.0.0, calling these functions with `digest` set to
`null` will print a deprecation warning to align with the behavior when `digest`
is `undefined`.

<a id="DEP0010"></a>
