<!-- YAML
added: v11.13.0
-->

* `emitter` {EventEmitter}
* `name` {string}
* 返回: {Promise}

创建一个 `Promise`，当 `EventEmitter` 触发给定的事件时则会被解决，当 `EventEmitter` 触发 `'error'` 时则会被拒绝。 
解决 `Promise` 时将会带上触发到给定事件的所有参数的数组。

此方法是有意通用的，并且可与 Web 平台的 [EventTarget][WHATWG-EventTarget] 接口一起使用，该接口没有特殊的 `'error'` 事件语义且不监听 `'error'` 事件。

```js
const { once, EventEmitter } = require('events');

async function run() {
  const ee = new EventEmitter();

  process.nextTick(() => {
    ee.emit('myevent', 42);
  });

  const [value] = await once(ee, 'myevent');
  console.log(value);

  const err = new Error('错误信息');
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











