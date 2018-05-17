
Type: Runtime

The embedded API provided by AsyncHooks exposes `.emitBefore()` and
`.emitAfter()` methods which are very easy to use incorrectly which can lead
to unrecoverable errors.

Use [`asyncResource.runInAsyncScope()`][] API instead which provides a much
safer, and more convenient, alternative. See
https://github.com/nodejs/node/pull/18513 for more details.

<a id="DEP0099"></a>
