<!-- YAML
added: v10.0.0
-->

* Returns: {boolean}

Returns `true` if the value is a generator object as returned from a
built-in generator function.
Note that this only reports back what the JavaScript engine is seeing;
in particular, the return value may not match the original source code if
a transpilation tool was used.

For example:

```js
function* foo() {}
const generator = foo();
util.types.isGeneratorObject(generator);  // Returns true
```

