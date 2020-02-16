<!-- YAML
added: v12.16.0
-->

* `name` {string} Name of the export to set.
* `value` {any} The value to set the export to.

This method is used after the module is linked to set the values of exports. If
it is called before the module is linked, an [`ERR_VM_MODULE_STATUS`][] error
will be thrown.

```js
const vm = require('vm');

(async () => {
  const m = new vm.SyntheticModule(['x'], () => {
    m.setExport('x', 1);
  });

  await m.link(() => {});
  await m.evaluate();

  assert.strictEqual(m.namespace.x, 1);
})();
```

