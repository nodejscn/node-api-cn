
从Node.js v0.10开始，[`dgram.Socket＃bind（）`][]更改为异步执行模型。旧代码采用同步行为，如下例所示：

```js
const s = dgram.createSocket('udp4');
s.bind(1234);
s.addMembership('224.0.0.114');
```

必须改为传递一个回调函数到[`dgram.Socket＃bind（）`][]：

```js
const s = dgram.createSocket('udp4');
s.bind(1234, () => {
  s.addMembership('224.0.0.114');
});
```

