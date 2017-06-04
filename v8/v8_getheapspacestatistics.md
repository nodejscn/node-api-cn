<!-- YAML
added: v6.0.0
changes:
  - version: v7.5.0
    pr-url: https://github.com/nodejs/node/pull/10186
    description: Support values exceeding the 32-bit unsigned integer range.
-->

Returns statistics about the V8 heap spaces, i.e. the segments which make up
the V8 heap. Neither the ordering of heap spaces, nor the availability of a
heap space can be guaranteed as the statistics are provided via the V8
[`GetHeapSpaceStatistics`][] function and may change from one V8 version to the
next.

The value returned is an array of objects containing the following properties:
* `space_name` {string}
* `space_size` {number}
* `space_used_size` {number}
* `space_available_size` {number}
* `physical_space_size` {number}

For example:

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

