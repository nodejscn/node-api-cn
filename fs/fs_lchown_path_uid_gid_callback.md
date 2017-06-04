<!-- YAML
deprecated: v0.4.7
changes:
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7897
    description: The `callback` parameter is no longer optional. Not passing
                 it will emit a deprecation warning.
-->

* `path` {string|Buffer}
* `uid` {integer}
* `gid` {integer}
* `callback` {Function}

异步的 lchown(2)。
完成回调只有一个可能的异常参数。

