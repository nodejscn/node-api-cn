
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!--name=vm-->

<!-- source_link=lib/vm.js -->

`vm` 模块使能够在 V8 虚拟机上下文中编译和运行代码。 
**`vm` 模块不是一个安全的机制。 
不要使用它来运行不受信任的代码。**

JavaScript 代码可以被立即地编译并且运行，或者编译、保存并且稍后运行。

一个常见的用例是在一个不同的 V8 上下文中运行代码。 
这意味着被调用的代码与调用的代码具有一个不同的全局对象。

通过[上下文隔离化][contextified]一个对象可以提供上下文。 
被调用的代码将上下文中的任何属性视为一个全局变量。 
由被调用的代码引起的对全局变量的任何更改都被反映在上下文对象中。

```js
const vm = require('vm');

const x = 1;

const context = { x: 2 };
vm.createContext(context); // 上下文隔离化该对象。

const code = 'x += 40; var y = 17;';
// `x` 和 `y` 是上下文中的全局变量。
// 最初，x 具有值 2，因为这是 context.x 的值。
vm.runInContext(code, context);

console.log(context.x); // 42
console.log(context.y); // 17

console.log(x); // 1; y 是未定义的。
```

