
Type: End-of-Life

`runInAsyncIdScope` doesn't emit the `'before'` or `'after'` event and can thus
cause a lot of issues. See https://github.com/nodejs/node/issues/14328 for more
details.

<a id="DEP0089"></a>
