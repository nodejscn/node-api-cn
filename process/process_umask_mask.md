<!-- YAML
added: v0.1.19
-->

* `mask` {number}

The `process.umask()` method sets or returns the Node.js process's file mode
creation mask. Child processes inherit the mask from the parent process. Invoked
without an argument, the current mask is returned, otherwise the umask is set to
the argument value and the previous mask is returned.

```js
const newmask = 0o022;
const oldmask = process.umask(newmask);
console.log(
  `Changed umask from ${oldmask.toString(8)} to ${newmask.toString(8)}`
);
```


