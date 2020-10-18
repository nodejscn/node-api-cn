<!-- YAML
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/17147
    description: End-of-Life.
  - version:
    - v9.4.0
    - v8.10.0
    pr-url: https://github.com/nodejs/node/pull/16972
    description: Runtime deprecation.
-->

Type: End-of-Life

`runInAsyncIdScope` doesn't emit the `'before'` or `'after'` event and can thus
cause a lot of issues. See <https://github.com/nodejs/node/issues/14328>.

