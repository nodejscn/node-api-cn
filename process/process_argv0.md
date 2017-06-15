<!-- YAML
added: 6.4.0
-->

* {string}

`process.argv0`属性，保存Node.js启动时传入的`argv[0]`参数值的一份只读副本。


```console
$ bash -c 'exec -a customArgv0 ./node'
> process.argv[0]
'/Volumes/code/external/node/out/Release/node'
> process.argv0
'customArgv0'
```
