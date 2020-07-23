
Event listeners registered for an event `type` may either be JavaScript
functions or objects with a `handleEvent` property whose value is a function.

In either case, the handler function will be invoked with the `event` argument
passed to the `eventTarget.dispatchEvent()` function.

Async functions may be used as event listeners. If an async handler function
rejects, the rejection will be captured and be will handled as described in
[`EventTarget` error handling][].

An error thrown by one handler function will not prevent the other handlers
from being invoked.

The return value of a handler function will be ignored.

Handlers are always invoked in the order they were added.

Handler functions may mutate the `event` object.

```js
function handler1(event) {
  console.log(event.type);  // Prints 'foo'
  event.a = 1;
}

async function handler2(event) {
  console.log(event.type);  // Prints 'foo'
  console.log(event.a);  // Prints 1
}

const handler3 = {
  handleEvent(event) {
    console.log(event.type);  // Prints 'foo'
  }
};

const handler4 = {
  async handleEvent(event) {
    console.log(event.type);  // Prints 'foo'
  }
};

const target = getEventTargetSomehow();

target.addEventListener('foo', handler1);
target.addEventListener('foo', handler2);
target.addEventListener('foo', handler3);
target.addEventListener('foo', handler4, { once: true });
```

