
* 返回 {AsyncHook} `asyncHook`的参照。

启用给定`AsyncHook`实例的回调。 如果没有提供回调，则启用操作是空操作。

`AsyncHook`实例默认是禁用的。如果`AsyncHook`实例应该在创建后立即启用，可以通过以下模式启用。

```js
const async_hooks = require('async_hooks');

const hook = async_hooks.createHook(callbacks).enable();
```

