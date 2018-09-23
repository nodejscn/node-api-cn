<!-- YAML
added: v10.0.0
-->
* `asyncFn` {Function|Promise}
* `error` {RegExp|Function}
* `message` {string}

Awaits the `asyncFn` promise or, if `asyncFn` is a function, immediately
calls the function and awaits the returned promise to complete. It will then
check that the promise is not rejected.

If `asyncFn` is a function and it throws an error synchronously,
`assert.doesNotReject()` will return a rejected `Promise` with that error. If
the function does not return a promise, `assert.doesNotReject()` will return a
rejected `Promise` with an [`ERR_INVALID_RETURN_VALUE`][] error. In both cases
the error handler is skipped.

Please note: Using `assert.doesNotReject()` is actually not useful because there
is little benefit by catching a rejection and then rejecting it again. Instead,
consider adding a comment next to the specific code path that should not reject
and keep error messages as expressive as possible.

If specified, `error` can be a [`Class`][], [`RegExp`][] or a validation
function. See [`assert.throws()`][] for more details.

Besides the async nature to await the completion behaves identically to
[`assert.doesNotThrow()`][].

```js
(async () => {
  await assert.doesNotReject(
    async () => {
      throw new TypeError('Wrong value');
    },
    SyntaxError
  );
})();
```

```js
assert.doesNotReject(Promise.reject(new TypeError('Wrong value')))
  .then(() => {
    // ...
  });
```

