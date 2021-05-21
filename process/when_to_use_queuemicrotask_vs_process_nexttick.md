
The [`queueMicrotask()`][] API is an alternative to `process.nextTick()` that
also defers execution of a function using the same microtask queue used to
execute the then, catch, and finally handlers of resolved promises. Within
Node.js, every time the "next tick queue" is drained, the microtask queue
is drained immediately after.

```js
Promise.resolve().then(() => console.log(2));
queueMicrotask(() => console.log(3));
process.nextTick(() => console.log(1));
// Output:
// 1
// 2
// 3
```

For *most* userland use cases, the `queueMicrotask()` API provides a portable
and reliable mechanism for deferring execution that works across multiple
JavaScript platform environments and should be favored over `process.nextTick()`.
In simple scenarios, `queueMicrotask()` can be a drop-in replacement for
`process.nextTick()`.

```js
console.log('start');
queueMicrotask(() => {
  console.log('microtask callback');
});
console.log('scheduled');
// Output:
// start
// scheduled
// microtask callback
```

One note-worthy difference between the two APIs is that `process.nextTick()`
allows specifying additional values that will be passed as arguments to the
deferred function when it is called. Achieving the same result with
`queueMicrotask()` requires using either a closure or a bound function:

```js
function deferred(a, b) {
  console.log('microtask', a + b);
}

console.log('start');
queueMicrotask(deferred.bind(undefined, 1, 2));
console.log('scheduled');
// Output:
// start
// scheduled
// microtask 3
```

There are minor differences in the way errors raised from within the next tick
queue and microtask queue are handled. Errors thrown within a queued microtask
callback should be handled within the queued callback when possible. If they are
not, the `process.on('uncaughtException')` event handler can be used to capture
and handle the errors.

When in doubt, unless the specific capabilities of `process.nextTick()` are
needed, use `queueMicrotask()`.

