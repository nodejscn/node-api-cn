<!-- YAML
added: v6.0.0
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10186
    description: Support values exceeding the 32-bit unsigned integer range.
-->

* 返回: {Object[]}

返回有关 V8 堆空间的统计信息，即组成 V8 堆的片段。
由于统计信息是通过 V8 的 [`GetHeapSpaceStatistics`] 函数提供的，因此可以保证堆空间的排序以及堆空间的可用性，并且可以从一个 V8 版本更改为下一个版本。

返回的值是包含以下属性的对象数组：
* `space_name` {string}
* `space_size` {number}
* `space_used_size` {number}
* `space_available_size` {number}
* `physical_space_size` {number}

```json
[
  {
    "space_name": "new_space",
    "space_size": 2063872,
    "space_used_size": 951112,
    "space_available_size": 80824,
    "physical_space_size": 2063872
  },
  {
    "space_name": "old_space",
    "space_size": 3090560,
    "space_used_size": 2493792,
    "space_available_size": 0,
    "physical_space_size": 3090560
  },
  {
    "space_name": "code_space",
    "space_size": 1260160,
    "space_used_size": 644256,
    "space_available_size": 960,
    "physical_space_size": 1260160
  },
  {
    "space_name": "map_space",
    "space_size": 1094160,
    "space_used_size": 201608,
    "space_available_size": 0,
    "physical_space_size": 1094160
  },
  {
    "space_name": "large_object_space",
    "space_size": 0,
    "space_used_size": 0,
    "space_available_size": 1490980608,
    "physical_space_size": 0
  }
]
```

