
> 稳定性: 2 - 稳定的

<!--name=vm-->

`vm` 模块提供了一系列 API 用于在 V8 虚拟机环境中编译和运行代码。
它可以通过以下方式使用：

```js
const vm = require('vm');
```

JavaScript 代码可以被编译并立即运行，或编译、保存然后再运行。

*注意*: vm模块并不是实现代码安全性的一套机制。The vm module is not a security mechanism.
**绝不要试图用其运行未经信任的代码**.

