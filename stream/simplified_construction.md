<!-- YAML
added: v1.2.0
-->

For many simple cases, it is possible to construct a stream without relying on
inheritance. This can be accomplished by directly creating instances of the
`stream.Writable`, `stream.Readable`, `stream.Duplex` or `stream.Transform`
objects and passing appropriate methods as constructor options.

For example:

```js
const { Writable } = require('stream');

const myWritable = new Writable({
  write(chunk, encoding, callback) {
    // ...
  }
});
```

