
浏览器兼容的 `URL` 类，根据 WHATWG URL 标准实现。[解析URL的示例][]可以在标准本身里边找到。

*注意*: 根据浏览器的约定，`URL` 对象的所有属性都是在类的原型上实现为getter和setter，而不是作为对象本身的数据属性。因此，与[遗留的urlObjects][]不同，在 `URL` 对象的任何属性(例如 `delete myURL.protocol`，`delete myURL.pathname`等)上使用 `delete` 关键字没有任何效果，但仍返回 `true`。
