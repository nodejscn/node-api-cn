<!-- YAML
added: v9.4.0
-->
- `eventName` {string|symbol}
- Returns: {Function[]}

Returns a copy of the array of listeners for the event named `eventName`,
including any wrappers (such as those created by `.once()`).

```js
const emitter = new EventEmitter();
emitter.once('log', () => console.log('log once'));

// Returns a new Array with a function `onceWrapper` which has a property
// `listener` which contains the original listener bound above
const listeners = emitter.rawListeners('log');
const logFnWrapper = listeners[0];

// logs "log once" to the console and does not unbind the `once` event
logFnWrapper.listener();

// logs "log once" to the console and removes the listener
logFnWrapper();

emitter.on('log', () => console.log('log persistently'));
// will return a new Array with a single function bound by `.on()` above
const newListeners = emitter.rawListeners('log');

// logs "log persistently" twice
newListeners[0]();
emitter.emit('log');
```

[`--trace-warnings`]: cli.html#cli_trace_warnings
[`EventEmitter.defaultMaxListeners`]: #events_eventemitter_defaultmaxlisteners
[`domain`]: domain.html
[`emitter.listenerCount()`]: #events_emitter_listenercount_eventname
[`emitter.removeListener()`]: #events_emitter_removelistener_eventname_listener
[`emitter.setMaxListeners(n)`]: #events_emitter_setmaxlisteners_n
[`fs.ReadStream`]: fs.html#fs_class_fs_readstream
[`net.Server`]: net.html#net_class_net_server
[`process.on('warning')`]: process.html#process_event_warning
[stream]: stream.html
