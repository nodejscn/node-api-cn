<!-- YAML
added: v0.9.1
-->

与`unref`相反, 在一个原先是`unref`的socket上调用 `ref` 将*不会*允许程序退出 
即使它是唯一剩下的socket（默认行为）。如果socket已经是`ref`的了，再次调用`ref`将
不会产生效果。

返回`socket`.

 