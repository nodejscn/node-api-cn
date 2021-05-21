
When writing to a writable stream from an async iterator, ensure correct
handling of backpressure and errors. [`stream.pipeline()`][] abstracts away
the handling of backpressure and backpressure-related errors:

```js
const fs = require('fs');
const { pipeline } = require('stream');
const { pipeline: pipelinePromise } = require('stream/promises');

const writable = fs.createWriteStream('./file');

// Callback Pattern
pipeline(iterator, writable, (err, value) => {
  if (err) {
    console.error(err);
  } else {
    console.log(value, 'value returned');
  }
});

// Promise Pattern
pipelinePromise(iterator, writable)
  .then((value) => {
    console.log(value, 'value returned');
  })
  .catch(console.error);
```

<!--type=misc-->

