<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17882
    description: End-of-Life.
  - version:
    - v6.12.0
    - v4.8.6
    pr-url: https://github.com/nodejs/node/pull/10116
    description: A deprecation code has been assigned.
  - version: v0.11.3
    commit: af80e7bc6e6f33c582eb1f7d37c7f5bbe9f910f7
    description: Documentation-only deprecation.
-->

Type: End-of-Life

The [`tls.CryptoStream`][] class was removed. Please use
[`tls.TLSSocket`][] instead.

