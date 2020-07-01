<!-- YAML
added: v14.5.0
-->

> Stability: 1 - Experimental

The `EventTarget` and `Event` objects are a Node.js-specific implementation
of the [`EventTarget` Web API][] that are exposed by some Node.js core APIs.
Neither the `EventTarget` nor `Event` classes are available for end
user code to create.

```js
const target = getEventTargetSomehow();

target.addEventListener('foo', (event) => {
  console.log('foo event happened!');
});
```

