
<!--introduced_in=v0.10.0-->

> 稳定性: 2 - 稳定的

<!--name=module-->

在 Node.js 模块系统中，每个文件被视为一个独立的模块。
例如，假设一个名为 `foo.js` 的文件：

```js
const circle = require('./circle.js');
console.log(`一个半径为 4 的圆的面积是 ${circle.area(4)}`);
```

在第一行中，`foo.js` 加载与 `foo.js` 在同一目录中的 `circle.js` 模块。

以下是 `circle.js` 的内容：

```js
const { PI } = Math;

exports.area = (r) => PI * r ** 2;

exports.circumference = (r) => 2 * PI * r;
```

`circle.js` 模块已经导出 `area()` 和 `circumference()` 函数。
通过在特殊的 `exports` 对象上指定其他的属性，函数和对象被添加到一个模块的根部。

模块本地的变量是私有的，因为模块被 Node.js 封装在一个函数中（查看[模块封装器][_module_wrapper]）。
在这个示例中，变量 `PI` 对 `circle.js` 是私有的。

`module.exports` 属性可以被分配一个新的值（例如一个函数或对象）。

下面，`bar.js` 使用了导出一个 Square 类的 `square` 模块：

```js
const Square = require('./square.js');
const mySquare = new Square(2);
console.log(`mySquare 的面积是 ${mySquare.area()}`);
```

`square` 模块被定义在 `square.js` 中：

```js
// 赋值给 exports 不会修改模块，必须使用 module.exports
module.exports = class Square {
  constructor(width) {
    this.width = width;
  }

  area() {
    return this.width ** 2;
  }
};
```

模块系统被实现在 `require('module')` 模块中。

