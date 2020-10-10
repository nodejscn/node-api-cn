<!-- YAML
added: v10.6.0
-->

* 返回: {Buffer}

创建一个可以被 `Script` 构造函数中 `cachedData` 选项使用的代码缓存。返回 `Buffer`。可以在任何时候不限次数地调用该方法。

```js
const script = new vm.Script(`
function add(a, b) {
  return a + b;
}

const x = add(1, 2);
`);

const cacheWithoutX = script.createCachedData();

script.runInThisContext();

const cacheWithX = script.createCachedData();
```

