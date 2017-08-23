<!-- YAML
added: v8.0.0
-->

Immediately close the session. All pending message callbacks will be called
with an error. [`session.connect()`] will need to be called to be able to send
messages again. Reconnected session will lose all inspector state, such as
enabled agents or configured breakpoints.


[`session.connect()`]: #inspector_session_connect
[`Debugger.paused`]: https://chromedevtools.github.io/devtools-protocol/v8/Debugger/#event-paused
[`EventEmitter`]: events.html#events_class_eventemitter
[Chrome DevTools Protocol Viewer]: https://chromedevtools.github.io/devtools-protocol/v8/
