
* 返回: {string}

在`URL`对象上调用`toString()`方法将返回序列化的URL。返回值与[`url.href`][]和[`url.toJSON()`][]的相同。

由于需要符合标准，此方法不允许用户自定义URL的序列化过程。 如果需要更大灵活性，[`require('url').format()`][]可能更合适。

