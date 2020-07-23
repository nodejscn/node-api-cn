
> 稳定性: 2 - 稳定

<!--name=vm-->

<!-- source_link=lib/vm.js -->

`vm` 模块可在 V8 虚拟机上下文中编译和运行代码。 
`vm` 模块不是安全的机制。 
不要使用它来运行不受信任的代码。

JavaScript 代码可以被立即编译并运行，也可以编译、保存并稍后运行。

一个常见的用例是在不同的 V8 上下文中运行代码。 
这意味着被调用的代码与调用的代码具有不同的全局对象。

可以通过使对象[上下文隔离化][contextified]来提供上下文。 
被调用的代码将上下文中的任何属性都视为全局变量。 
由调用的代码引起的对全局变量的任何更改都将会反映在上下文对象中。

```js
const vm = require('vm');

const x = 1;

const context = { x: 2 };
vm.createContext(context); // 上下文隔离化对象。

const code = 'x += 40; var y = 17;';
// `x` and `y` 是上下文中的全局变量。
// 最初，x 的值为 2，因为这是 context.x 的值。
vm.runInContext(code, context);

console.log(context.x); // 42
console.log(context.y); // 17

console.log(x); // 1; y 没有定义。
```

