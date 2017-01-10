
* `fn` {Function}
* `...args` {any}

Run the supplied function in the context of the domain, implicitly
binding all event emitters, timers, and lowlevel requests that are
created in that context. Optionally, arguments can be passed to
the function.

This is the most basic way to use a domain.

Example:

```js
const domain = require('domain');
const fs = require('fs');
const d = domain.create();
d.on('error', (er) => {
  console.error('Caught error!', er);
});
d.run(() => {
  process.nextTick(() => {
    setTimeout(() => { // simulating some various async stuff
      fs.open('non-existent file', 'r', (er, fd) => {
        if (er) throw er;
        // proceed...
      });
    }, 100);
  });
});
```

In this example, the `d.on('error')` handler will be triggered, rather
than crashing the program.

