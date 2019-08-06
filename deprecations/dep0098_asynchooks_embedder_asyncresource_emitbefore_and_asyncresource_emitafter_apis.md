<!-- YAML
changes:
  - version: v12.0.0
    pr-url: https://github.com/nodejs/node/pull/26530
    description: End-of-Life
  - version:
    - v8.12.0
    - v9.6.0
    - v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18632
    description: Runtime deprecation.
-->

Type: End-of-Life

The embedded API provided by AsyncHooks exposes `.emitBefore()` and
`.emitAfter()` methods which are very easy to use incorrectly which can lead
to unrecoverable errors.

Use [`asyncResource.runInAsyncScope()`][] API instead which provides a much
safer, and more convenient, alternative. See
<https://github.com/nodejs/node/pull/18513>.

<a id="DEP0099"></a>
