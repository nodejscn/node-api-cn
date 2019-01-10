<!-- YAML
added: v0.3.1
-->

* `sandbox` {Object}

给定一个`sandbox`对象， `vm.createContext()`会[设置此`sandbox`][contextified]，从而让它具备在[`vm.runInContext()`][]或者[`script.runInContext()`][]中被使用的能力。对于此二方法中所调用的脚本，他们的全局对象不仅拥有我们提供的`sandbox`对象的所有属性，同时还有任何[global object][]所拥有的属性。对于这些脚本之外的所有代码，他们的全局变量将保持不变。

```js
const util = require('util');
const vm = require('vm');

global.globalVar = 3;

const sandbox = { globalVar: 1 };
vm.createContext(sandbox);

vm.runInContext('globalVar *= 2;', sandbox);

console.log(util.inspect(sandbox)); // { globalVar: 2 }

console.log(util.inspect(globalVar)); // 3
```

如果未提供`sandbox`（或者传入`undefined`），那么会返回一个全新的，空的，[上下文隔离化][contextified]后的`sandbox`对象。

`vm.createContext()`主要是用于创建一个能运行多个脚本的`sandbox`。比如说，在模拟一个网页浏览器时，此方法可以被用于创建一个单独的`sandbox`来代表一个窗口的全局对象，然后所有的`<script>`标签都可以在这个`sandbox`的上下文中运行。

