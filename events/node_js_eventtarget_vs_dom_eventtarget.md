
There are two key differences between the Node.js `EventTarget` and the
[`EventTarget` Web API][]:

1. Whereas DOM `EventTarget` instances *may* be hierarchical, there is no
   concept of hierarchy and event propagation in Node.js. That is, an event
   dispatched to an `EventTarget` does not propagate through a hierarchy of
   nested target objects that may each have their own set of handlers for the
   event.
2. In the Node.js `EventTarget`, if an event listener is an async function
   or returns a `Promise`, and the returned `Promise` rejects, the rejection
   is automatically captured and handled the same way as a listener that
   throws synchronously (see [`EventTarget` error handling][] for details).

