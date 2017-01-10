<!-- YAML
added: v0.9.2
-->

* Returns: {Object}

Returns a JSON representation of `buf`. [`JSON.stringify()`] implicitly calls
this function when stringifying a `Buffer` instance.

Example:

```js
const buf = Buffer.from([0x1, 0x2, 0x3, 0x4, 0x5]);
const json = JSON.stringify(buf);

// Prints: {"type":"Buffer","data":[1,2,3,4,5]}
console.log(json);

const copy = JSON.parse(json, (key, value) => {
  return value && value.type === 'Buffer'
    ? Buffer.from(value.data)
    : value;
});

// Prints: <Buffer 01 02 03 04 05>
console.log(copy);
```

