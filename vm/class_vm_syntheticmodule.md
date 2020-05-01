<!-- YAML
added:
 - v13.0.0
 - v12.16.0
-->

> Stability: 1 - Experimental

*This feature is only available with the `--experimental-vm-modules` command
flag enabled.*

* Extends: {vm.Module}

The `vm.SyntheticModule` class provides the [Synthetic Module Record][] as
defined in the WebIDL specification. The purpose of synthetic modules is to
provide a generic interface for exposing non-JavaScript sources to ECMAScript
module graphs.

```js
const vm = require('vm');

const source = '{ "a": 1 }';
const module = new vm.SyntheticModule(['default'], function() {
  const obj = JSON.parse(source);
  this.setExport('default', obj);
});

// Use `module` in linking...
```

