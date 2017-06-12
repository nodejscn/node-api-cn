
<!-- type=misc -->

对象可以定义自己的 `[util.inspect.custom](depth, opts)`（或 `inspect(depth, opts)`） 函数，`util.inspect()` 会调用并使用查看对象时的结果：

```js
const util = require('util');

class Box {
  constructor(value) {
    this.value = value;
  }

  inspect(depth, options) {
    if (depth < 0) {
      return options.stylize('[Box]', 'special');
    }

    const newOptions = Object.assign({}, options, {
      depth: options.depth === null ? null : options.depth - 1
    });

    // 五个空格的填充，因为那是 "Box< " 的大小。
    const padding = ' '.repeat(5);
    const inner = util.inspect(this.value, newOptions)
                      .replace(/\n/g, `\n${padding}`);
    return `${options.stylize('Box', 'special')}< ${inner} >`;
  }
}

const box = new Box(true);

util.inspect(box);
// 返回: "Box< true >"
```

自定义的 `[util.inspect.custom](depth, opts)` 函数通常返回一个字符串，但也可以返回一个任何类型的值，它会相应地被 `util.inspect()` 格式化。

```js
const util = require('util');

const obj = { foo: '这个不会出现在 inspect() 的输出中' };
obj[util.inspect.custom] = function(depth) {
  return { bar: 'baz' };
};

util.inspect(obj);
// 返回: "{ bar: 'baz' }"
```

一个自定义的查看方法可以通过在一个对象上开放一个 `inspect(depth, opts)` 方法来提供：

```js
const util = require('util');

const obj = { foo: '这个不会出现在 inspect() 的输出中' };
obj.inspect = function(depth) {
  return { bar: 'baz' };
};

util.inspect(obj);
// 返回: "{ bar: 'baz' }"
```

