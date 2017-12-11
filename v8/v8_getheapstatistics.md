<!-- YAML
added: v1.0.0
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/8610
    description: 新增 `malloced_memory`, `peak_malloced_memory`,
                 和 `does_zap_garbage`.
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10186
    description: 新增对超过32位的非符号整型的支持
-->

返回拥有以下参数的对象：

* `total_heap_size` {number}
* `total_heap_size_executable` {number}
* `total_physical_size` {number}
* `total_available_size` {number}
* `used_heap_size` {number}
* `heap_size_limit` {number}
* `malloced_memory` {number}
* `peak_malloced_memory` {number}
* `does_zap_garbage` {number}

`does_zap_garbage`是个0/1式布尔值，它凸显是否设置了`--zap_code_space`选项。若为真，那么V8引擎会用一个位模式来覆盖堆中的垃圾。如此，RSS(常驻内存集)会变得越来越大，因为V8会一直征用所有的堆页，从而让他们更难被操作系统交换掉。

For example:

<!-- eslint-skip -->
```js
{
  total_heap_size: 7326976,
  total_heap_size_executable: 4194304,
  total_physical_size: 7326976,
  total_available_size: 1152656,
  used_heap_size: 3476208,
  heap_size_limit: 1535115264,
  malloced_memory: 16384,
  peak_malloced_memory: 1127496,
  does_zap_garbage: 0
}
```

