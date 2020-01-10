<!-- YAML
added: v1.0.0
changes:
  - version: v7.2.0
    pr-url: https://github.com/nodejs/node/pull/8610
    description: Added `malloced_memory`, `peak_malloced_memory`,
                 and `does_zap_garbage`.
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10186
    description: Support values exceeding the 32-bit unsigned integer range.

  - version: v12.4.0
    pr-url: https://github.com/nodejs/node/pull/27933
    description: 增加 number_of_native_contexts 和 number_of_detached_contexts 新属性.
-->

* 返回: {Object}

返回具有以下属性的对象：

* `total_heap_size` {number}
* `total_heap_size_executable` {number}
* `total_physical_size` {number}
* `total_available_size` {number}
* `used_heap_size` {number}
* `heap_size_limit` {number}
* `malloced_memory` {number}
* `peak_malloced_memory` {number}
* `does_zap_garbage` {number}
* `number_of_native_contexts` {number}
* `number_of_detached_contexts` {number}

`does_zap_garbage` 是一个 0/1 布尔值，表示是否启用了 `--zap_code_space` 选项。 
这使得 V8 用位模式覆盖堆垃圾。 
RSS 占用空间（常驻内存集）会变得越来越大，因为它不断触及所有堆页面，这使得它们不太可能被操作系统交换出。

`number_of_native_contexts` native_context 的值是当前活动的顶层上下文的数量。 
随着时间的推移，此数字的增加表示内存泄漏。

`number_of_detached_contexts` detached_context 的值是已分离但尚未回收垃圾的上下文数。
该数字不为零表示潜在的内存泄漏。

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
  does_zap_garbage: 0,
  number_of_native_contexts: 1,
  number_of_detached_contexts: 0
}
```

