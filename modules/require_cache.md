<!-- YAML
added: v0.3.0
-->

* {Object}

被引入的模块将被缓存在这个对象中。
从此对象中删除键值对将会导致下一次 `require` 重新加载被删除的模块。
这不适用于[原生插件][native addons]，因为它们的重载将会导致错误。

可以添加或替换入口。 
在加载原生模块之前会检查此缓存，如果将与原生模块匹配的名称添加到缓存中，则引入调用将不再获取原生模块。 
谨慎使用！

<!-- eslint-disable node-core/no-duplicate-requires -->
```js
const assert = require('assert');
const realFs = require('fs');

const fakeFs = {};
require.cache.fs = { exports: fakeFs };

assert.strictEqual(require('fs'), fakeFs);
assert.strictEqual(require('node:fs'), realFs);
```



