<!-- YAML
added: v6.4.0
-->

* {string}

`process.argv0` 属性保存当 Node.js 启动时传入的 `argv[0]` 的原始值的只读副本。

```console
$ bash -c 'exec -a customArgv0 ./node'
> process.argv[0]
'/Volumes/code/external/node/out/Release/node'
> process.argv0
'customArgv0'
```

