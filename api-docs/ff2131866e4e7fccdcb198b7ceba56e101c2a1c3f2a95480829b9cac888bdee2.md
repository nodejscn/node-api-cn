<!-- YAML
added: v10.16.0
-->
* `emitter` {EventEmitter}
* `name` {string}
* Returns: {Promise}

Creates a `Promise` that is resolved when the `EventEmitter` emits the given
event or that is rejected when the `EventEmitter` emits `'error'`.
The `Promise` will resolve with an array of all the arguments emitted to the
given event.

```js
const { once, EventEmitter } = require('events');

async function run() {
  const ee = new EventEmitter();

  process.nextTick(() => {
    ee.emit('myevent', 42);
  });

  const [value] = await once(ee, 'myevent');
  console.log(value);

  const err = new Error('kaboom');
  process.nextTick(() => {
    ee.emit('error', err);
  });

  try {
    await once(ee, 'myevent');
  } catch (err) {
    console.log('error happened', err);
  }
}

run();
```











