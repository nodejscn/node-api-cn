<!-- YAML
added: v0.1.19
-->

* `mask` {number}

The `process.umask()` method sets or returns the Node.js process's file mode
creation mask. Child processes inherit the mask from the parent process. The old
mask is return if the `mask` argument is given, otherwise returns the current
mask.

```js
const newmask = 0o022;
const oldmask = process.umask(newmask);
console.log(
  `Changed umask from ${oldmask.toString(8)} to ${newmask.toString(8)}`
);
```


