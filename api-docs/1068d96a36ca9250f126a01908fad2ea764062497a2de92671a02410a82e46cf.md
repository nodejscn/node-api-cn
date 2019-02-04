<!-- YAML
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/9744
    description: Errors that occur while writing to the underlying streams
                 will now be ignored by default.
-->

<!--type=class-->

`Console` 类可用于创建具有可配置的输出流的简单记录器，可以使用 `require('console').Console` 或 `console.Console`（或其结构化对应物）访问：

```js
const { Console } = require('console');
```

```js
const { Console } = console;
```

