<!-- YAML
added: v8.5.0
-->

* `src` {string|Buffer|URL} 要被拷贝的源文件名称
* `dest` {string|Buffer|URL} 拷贝操作的目标文件名
* `flags` {number} 拷贝操作修饰符 **默认:** `0`
* `callback` {Function}

异步的将 `src` 拷贝到 `dest`。Asynchronously copies `src` to `dest`. 默认情况下，如果 `dest` 已经存在会被覆盖。回调函数没有给出除了异常以外的参数。Node.js 不能保证拷贝操作的原子性。如果目标文件打开后出现错误，Node.js 将尝试删除它。

`flags` 是一个可选的整数，用于指定行为的拷贝操作。唯一支持的 flag 是 `fs.constants.COPYFILE_EXCL` ，如果 `dest` 已经存在，则会导致拷贝操作失败。

例:

```js
const fs = require('fs');

// 默认情况下，destination.txt 将创建或覆盖
fs.copyFile('source.txt', 'destination.txt', (err) => {
  if (err) throw err;
  console.log('source.txt was copied to destination.txt');
});
```

如果第三个参数是数字，那么肯定是 `flags`，代码如下所示:  

```js
const fs = require('fs');
const { COPYFILE_EXCL } = fs.constants;

// 使用 COPYFILE_EXCL ，如果 destination.txt 文件存在，操作将失败。
fs.copyFile('source.txt', 'destination.txt', COPYFILE_EXCL, callback);
```

