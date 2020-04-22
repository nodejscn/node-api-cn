
Redirected dependencies can provide attenuated or modified functionality as fits
the application. For example, log data about timing of function durations by
wrapping the original:

```js
const original = require('fn');
module.exports = function fn(...args) {
  console.time();
  try {
    return new.target ?
      Reflect.construct(original, args) :
      Reflect.apply(original, this, args);
  } finally {
    console.timeEnd();
  }
};
```


