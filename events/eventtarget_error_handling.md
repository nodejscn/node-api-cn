
When a registered event listener throws (or returns a Promise that rejects),
by default the error will be forwarded to the `process.on('error')` event
on `process.nextTick()`. Throwing within an event listener will *not* stop
the other registered handlers from being invoked.

The `EventTarget` does not implement any special default handling for
`'error'` type events.

