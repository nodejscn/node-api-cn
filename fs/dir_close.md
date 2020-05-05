<!-- YAML
added: v12.12.0
-->

* 返回: {Promise}

异步地关闭目录的底层资源句柄。 
后续的读取会导致错误。

返回 `Promise`（在资源被关闭之后会被 resolve）。

