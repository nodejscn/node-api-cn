<!-- YAML
added: v10.5.0
-->

* {boolean}

Is `true` if this code is not running inside of a [`Worker`][] thread.

```js
const { Worker, isMainThread } = require('worker_threads');

if (isMainThread) {
  // This re-loads the current file inside a Worker instance.
  new Worker(__filename);
} else {
  console.log('Inside Worker!');
  console.log(isMainThread);  // Prints 'false'.
}
```

