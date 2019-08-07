
> 稳定性: 2 - 稳定

<!--name=vm-->

`vm` 模块提供了在 V8 虚拟机上下文中编译和运行代码的一系列 API。`vm` 模块不是一个安全的虚拟机。不要用它来运行不受信任的代码。在这些文档中 "sanbox" 这个术语仅仅是为了表示一个单独的上下文，并不提供任何安全保障。

JavaScript 代码可以被编译并立即运行，也可以编译、保存，以后再运行。

一个常见的场景是在沙盒中运行代码。沙盒中的代码使用不同的 V8 上下文，这意味着它具有与其余代码不同的全局对象。

可以通过[上下文隔离化][contextified]一个沙箱对象来提供上下文。沙盒代码将沙盒中的任何属性视为全局对象。由沙盒代码引起的任何全局变量的更改都将反映到沙盒对象中。


```js
const vm = require('vm');

const x = 1;

const sandbox = { x: 2 };
vm.createContext(sandbox); // 上下文隔离化一个沙盒。

const code = 'x += 40; var y = 17;';
// `x` and `y` 是沙盒环境中的全局变量。
// 最初，x 的值为 2，因为这是 sandbox.x 的值。
vm.runInContext(code, sandbox);

console.log(sandbox.x); // 42
console.log(sandbox.y); // 17

console.log(x); // 1; y 没有定义。
```

