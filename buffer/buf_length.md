<!-- YAML
added: v0.1.90
-->

* {Integer}

Returns the amount of memory allocated for `buf` in bytes. Note that this
does not necessarily reflect the amount of "usable" data within `buf`.

Example: Create a `Buffer` and write a shorter ASCII string to it

```js
const buf = Buffer.alloc(1234);

// Prints: 1234
console.log(buf.length);

buf.write('some string', 0, 'ascii');

// Prints: 1234
console.log(buf.length);
```

While the `length` property is not immutable, changing the value of `length`
can result in undefined and inconsistent behavior. Applications that wish to
modify the length of a `Buffer` should therefore treat `length` as read-only and
use [`buf.slice()`] to create a new `Buffer`.

Examples:

```js
var buf = Buffer.allocUnsafe(10);

buf.write('abcdefghj', 0, 'ascii');

// Prints: 10
console.log(buf.length);

buf = buf.slice(0, 5);

// Prints: 5
console.log(buf.length);
```

