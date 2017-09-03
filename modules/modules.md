
> 稳定性: 2 - 稳定的

<!--name=module-->

Node.js 有一个简单的模块加载系统。
在 Node.js 中，文件和模块是一一对应的（每个文件被视为一个独立的模块）。

例子，假设有一个名为 `foo.js` 的文件：

```js
const circle = require('./circle.js');
console.log(`半径为 4 的圆的面积是 ${circle.area(4)}`);
```

在第一行中，`foo.js` 加载了同一目录下的 `circle.js` 模块。

`circle.js` 文件的内容为：

```js
const { PI } = Math;

exports.area = (r) => PI * r ** 2;

exports.circumference = (r) => 2 * PI * r;
```

`circle.js` 模块导出了 `area()` 和 `circumference()` 两个函数。
通过在特殊的 `exports` 对象上指定额外的属性，函数和对象可以被添加到模块的根部。

模块内的本地变量是私有的，因为模块被 Node.js 包装在一个函数中（详见[模块包装器]）。
在这个例子中，变量 `PI` 是 `circle.js` 私有的。

`module.exports`属性可以被赋予一个新的值（例如函数或对象）。

如下，`bar.js` 会用到 `square` 模块，`square` 导出一个构造函数：

```js
const square = require('./square.js');
const mySquare = square(2);
console.log(`正方形的面积是 ${mySquare.area()}`);
```

`square` 模块定义在 `square.js` 中：

```js
// 赋值给 `exports` 不会修改模块，必须使用 `module.exports`
module.exports = (width) => {
  return {
    area: () => width ** 2
  };
};
```

模块系统在 `require('module')` 模块中实现。

