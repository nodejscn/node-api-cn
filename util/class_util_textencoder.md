<!-- YAML
added: v8.3.0
changes:
  - version: v11.0.0
    pr-url: v11.0.0
    description: The class is now available on the global object.
-->

An implementation of the [WHATWG Encoding Standard][] `TextEncoder` API. All
instances of `TextEncoder` only support UTF-8 encoding.

```js
const encoder = new TextEncoder();
const uint8array = encoder.encode('this is some data');
```

The `TextEncoder` class is also available on the global object.

