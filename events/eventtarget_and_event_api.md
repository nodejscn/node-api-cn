<!-- YAML
added: v14.5.0
changes:
  - version: v16.0.0
    pr-url: https://github.com/nodejs/node/pull/37237
    description: changed EventTarget error handling.
  - version: v15.4.0
    pr-url: https://github.com/nodejs/node/pull/35949
    description: No longer experimental.
  - version: v15.0.0
    pr-url: https://github.com/nodejs/node/pull/35496
    description:
      The `EventTarget` and `Event` classes are now available as globals.
-->

The `EventTarget` and `Event` objects are a Node.js-specific implementation
of the [`EventTarget` Web API][] that are exposed by some Node.js core APIs.

```js
const target = new EventTarget();

target.addEventListener('foo', (event) => {
  console.log('foo event happened!');
});
```

