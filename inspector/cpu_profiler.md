
Apart from the debugger, various V8 Profilers are available through the DevTools
protocol. Here's a simple example showing how to use the [CPU profiler][]:

```js
const inspector = require('inspector');
const fs = require('fs');
const session = new inspector.Session();
session.connect();

session.post('Profiler.enable', () => {
  session.post('Profiler.start', () => {
    // invoke business logic under measurement here...

    // some time later...
    session.post('Profiler.stop', (err, { profile }) => {
      // write profile to disk, upload, etc.
      if (!err) {
        fs.writeFileSync('./profile.cpuprofile', JSON.stringify(profile));
      }
    });
  });
});
```

[`'Debugger.paused'`]: https://chromedevtools.github.io/devtools-protocol/v8/Debugger#event-paused
[`EventEmitter`]: events.html#events_class_eventemitter
[`session.connect()`]: #inspector_session_connect
[Chrome DevTools Protocol Viewer]: https://chromedevtools.github.io/devtools-protocol/v8/
[CPU Profiler]: https://chromedevtools.github.io/devtools-protocol/v8/Profiler
