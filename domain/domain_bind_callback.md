
* `callback` {Function} The callback function
* Returns: {Function} The bound function

The returned function will be a wrapper around the supplied callback
function. When the returned function is called, any errors that are
thrown will be routed to the domain's `'error'` event.

```js
const d = domain.create();

function readSomeFile(filename, cb) {
  fs.readFile(filename, 'utf8', d.bind((er, data) => {
    // If this throws, it will also be passed to the domain.
    return cb(er, data ? JSON.parse(data) : null);
  }));
}

d.on('error', (er) => {
  // An error occurred somewhere. If we throw it now, it will crash the program
  // with the normal line number and stack message.
});
```

