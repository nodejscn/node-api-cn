<!-- YAML
added: v11.13.0
-->
* `emitter` {EventEmitter}
* `name` {string}
* 返回: {Promise}

创建一个 `Promise`，当 `EventEmitter` 触发给定的事件时则会被解决，当 `EventEmitter` 触发 `'error'` 时则会被拒绝。 
解决 `Promise` 时将会带上触发到给定事件的所有参数的数组。

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
    console.log('出错', err);
  }
}

run();
```











