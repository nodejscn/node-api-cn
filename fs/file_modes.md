
`mode` 参数会在 `fs.chmod()` 和 `fs.chmodSync()`方法中用到，它是用下面的常量进行逻辑或(logical OR)操作后的数字掩码：


|       Constant         |  Octal  | Description              |
| ---------------------- | ------- | ------------------------ |
| `fs.constants.S_IRUSR` | `0o400` | read by owner            |
| `fs.constants.S_IWUSR` | `0o200` | write by owner           |
| `fs.constants.S_IXUSR` | `0o100` | execute/search by owner  |
| `fs.constants.S_IRGRP` | `0o40`  | read by group            |
| `fs.constants.S_IWGRP` | `0o20`  | write by group           |
| `fs.constants.S_IXGRP` | `0o10`  | execute/search by group  |
| `fs.constants.S_IROTH` | `0o4`   | read by others           |
| `fs.constants.S_IWOTH` | `0o2`   | write by others          |
| `fs.constants.S_IXOTH` | `0o1`   | execute/search by others |

一个构造 `mode` 的更简单的方式是使用3位八进制串（比如，765）。最左侧的数字（例中的7）代表了文件所有者的权限。中间一位（例中的6）代表了组的权限。最右侧的数字（例中的5）代表其他人的权限。
A

| Number  |       Description        |
| ------- | ------------------------ |
|   `7`   | read, write, and execute |
|   `6`   | read and write           |
|   `5`   | read and execute         |
|   `4`   | read only                |
|   `3`   | write and execute        |
|   `2`   | write only               |
|   `1`   | execute only             |
|   `0`   | no permission            |

举个例子，八进制值 `0o765` 表示：

* 文件所有者可以进行读、写和执行。
* 文件所属组可以读和写。
* 其他人可以对文件进行读和执行。

