
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定

<!--name=module-->

在 Node.js 模块系统中，每个文件都被视为一个独立的模块。
例如，假设有一个名为 `foo.js` 的文件：

```js
const circle = require('./circle.js');
console.log(`半径为 4 的圆的面积是 ${circle.area(4)}`);
```

在第一行中，`foo.js` 加载了与 `foo.js` 在同一目录中的 `circle.js` 模块。

以下是 `circle.js` 的内容：

```js
const { PI } = Math;

exports.area = (r) => PI * r ** 2;

exports.circumference = (r) => 2 * PI * r;
```

`circle.js` 模块导出了 `area()` 和 `circumference()` 函数。
通过在特殊的 `exports` 对象上指定额外的属性，可以将函数和对象添加到模块的根部。

模块内的本地变量是私有的，因为模块由 Node.js 封装在一个函数中（详见[模块封装器]）。
在这个例子中，变量 `PI` 对 `circle.js` 是私有的。

可以为 `module.exports` 属性分配新的值（例如函数或对象）。

下面的例子中，`bar.js` 使用了导出 Square 类的 `square` 模块：

```js
const Square = require('./square.js');
const mySquare = new Square(2);
console.log(`mySquare 的面积是 ${mySquare.area()}`);
```

`square` 模块定义在 `square.js` 中：

```js
// 赋值给 `exports` 不会修改模块，必须使用 `module.exports`。
module.exports = class Square {
  constructor(width) {
    this.width = width;
  }

  area() {
    return this.width ** 2;
  }
};
```

模块系统在 `require('module')` 模块中实现。

