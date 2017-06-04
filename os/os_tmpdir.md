<!-- YAML
added: v0.9.9
changes:
  - version: v2.0.0
    pr-url: https://github.com/nodejs/node/pull/747
    description: This function is now cross-platform consistent and no longer
                 returns a path with a trailing slash on any platform
-->

* Returns: {string}

`os.tmpdir()`方法返回一个字符串, 表明操作系统的
默认临时文件目录.

