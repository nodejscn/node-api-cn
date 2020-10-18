<!-- YAML
changes:
  - version: v12.8.0
    pr-url: https://github.com/nodejs/node/pull/28892
    description: Deprecation revoked.
  - version:
      - v9.9.0
      - v8.13.0
    pr-url: https://github.com/nodejs/node/pull/17002
    description: Documentation-only deprecation.
-->

Type: Deprecation revoked

Importing assert directly was not recommended as the exposed functions use
loose equality checks. The deprecation was revoked because use of the `assert`
module is not discouraged, and the deprecation caused developer confusion.

