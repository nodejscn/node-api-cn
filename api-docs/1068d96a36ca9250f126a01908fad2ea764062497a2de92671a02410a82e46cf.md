<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: Errors that occur while writing to the underlying streams
                 will now be ignored.
-->

<!--type=class-->

`Console` 类可用于创建一个具有可配置的输出流的简单记录器，可以通过 `require('console').Console` 或 `console.Console` 使用：

```js
const { Console } = require('console');
```

```js
const { Console } = console;
```

