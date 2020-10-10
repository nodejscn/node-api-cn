<!-- YAML
added: v8.0.0
-->
* `label` {string}

除非在检查器中使用，否则此方法不显示任何内容。 
`console.profile()` 方法启动带有可选标签的 JavaScript CPU 配置文件，直到调用 [`console.profileEnd()`]。 
然后将配置文件添加到检查器的 Profiles 面板中。

```js
console.profile('MyLabel');
// 一些代码
console.profileEnd('MyLabel');
// 将配置文件 'MyLabel' 添加到检查器的 Profiles 面板中。
```

