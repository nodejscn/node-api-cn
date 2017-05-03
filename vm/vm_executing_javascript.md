
> 稳定性: 2 - 稳定的

<!--name=vm-->

`vm` 模块提供了一系列 API 用于在 V8 虚拟机环境中编译和运行代码。
它可以通过以下方式使用：

```js
const vm = require('vm');
```

JavaScript 代码可以被编译并立即运行，或编译、保存然后再运行。

*Note*: The vm module is not a security mechanism.
**Do not use it to run untrusted code**.

