<!-- YAML
added: v13.4.0
-->

> Stability: 1 - captureRejections is experimental.

* `err` Error
* `eventName` {string|symbol}
* `...args` {any}

The `Symbol.for('nodejs.rejection')` method is called in case a
promise rejection happens when emitting an event and
[`captureRejections`][capturerejections] is enabled on the emitter.
It is possible to use [`events.captureRejectionSymbol`][rejectionsymbol] in
place of `Symbol.for('nodejs.rejection')`.

```js
const { EventEmitter, captureRejectionSymbol } = require('events');

class MyClass extends EventEmitter {
  constructor() {
    super({ captureRejections: true });
  }

  [captureRejectionSymbol](err, event, ...args) {
    console.log('rejection happened for', event, 'with', err, ...args);
    this.destroy(err);
  }

  destroy(err) {
    // Tear the resource down here.
  }
}
```

