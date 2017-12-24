
> 稳定性: 2 - 稳定的

<!--name=vm-->

`vm` 模块提供了一系列 API 用于在 V8 虚拟机环境中编译和运行代码。

JavaScript 代码可以被编译并立即运行，或编译、保存然后再运行。

A common use case is to run the code in a sandboxed environment.
The sandboxed code uses a different V8 Context, meaning that
it has a different global object than the rest of the code.

One can provide the context by ["contextifying"][contextified] a sandbox
object. The sandboxed code treats any property on the sandbox like a
global variable. Any changes on global variables caused by the sandboxed
code are reflected in the sandbox object.

```js
const vm = require('vm');

const x = 1;

const sandbox = { x: 2 };
vm.createContext(sandbox); // Contextify the sandbox.

const code = 'x += 40; var y = 17;';
// x and y are global variables in the sandboxed environment.
// Initially, x has the value 2 because that is the value of sandbox.x.
vm.runInContext(code, sandbox);

console.log(sandbox.x); // 42
console.log(sandbox.y); // 17

console.log(x); // 1; y is not defined.
```

*注意*: vm模块并不是实现代码安全性的一套机制。
**绝不要试图用其运行未经信任的代码**.

