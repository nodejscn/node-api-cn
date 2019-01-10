<!-- YAML
added: v6.0.0
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10186
    description: Support values exceeding the 32-bit unsigned integer range.
-->

返回关于v8堆空间的统计,即组成v8堆的片段。通过V8 [`GetHeapSpaceStatistics`][] 函数提供统计信息，无论堆空间的顺序，或是堆空间的可用性都可以被保证，并且可能是多个V8版本。

返回一个数组包含如下属性：
* `space_name` {string}
* `space_size` {number}
* `space_used_size` {number}
* `space_available_size` {number}
* `physical_space_size` {number}

例如:

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

