<!-- YAML
added:
  - v7.0.0
  - v6.13.0
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18281
    description: 该类现在在全局的对象上是可用的。
-->

浏览器兼容的 `URL` 类，通过遵循 WHATWG URL 标准实现。
[解析的 URL 的示例][Examples of parsed URLs]可以在该标准自身中被找到。
`URL` 类也是在全局的对象上可用的。

根据浏览器的约定，`URL` 对象的所有属性都被实现为类的原型上的获取器和设置器，而不是作为对象自身上的数据属性。
因此，不同于[旧版的 `urlObject`][legacy `urlObject`]，在 `URL` 对象的任何属性上使用 `delete` 关键字没有效果（例如 `delete myURL.protocol`、`delete myURL.pathname` 等），但是仍然返回 `true`。

