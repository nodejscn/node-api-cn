
When writing to a writable stream from an async iterator, ensure correct
handling of backpressure and errors. [`stream.pipeline()`][] abstracts away
the handling of backpressure and backpressure-related errors:

```js
const { pipeline } = require('stream');
const util = require('util');
const fs = require('fs');

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
const pipelinePromise = util.promisify(pipeline);
pipelinePromise(iterator, writable)
  .then((value) => {
    console.log(value, 'value returned');
  })
  .catch(console.error);
```

<!--type=misc-->

