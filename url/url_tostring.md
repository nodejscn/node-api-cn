
* Returns: {string}

`URL`对象上的`toString()`方法返回序列化的URL。返回值与[`url.href`][] 和 [`url.toJSON()`][]的相同。

因为需要符合标准，该方法不允许用户自定义URL系列化进程。如果需要更大的灵活性，请查看[`require('url').format()`][] 方法。

