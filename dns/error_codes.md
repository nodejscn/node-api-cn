每个DNS查询可以返回一个错误代码如下:

*   `dns.NODATA`: DNS服务返回没有数据.
*   `dns.FORMERR`: DNS服务器查询没有格式化.
*   `dns.SERVFAIL`: DNS服务器返回失败。
*   `dns.NOTFOUND`: 域名未找到。
*   `dns.NOIMP`: DNS服务器不执行请求的操作。
*   `dns.REFUSED`: 查询DNS服务器拒绝。
*   `dns.BADQUERY`:  未格式化DNS查询。
*   `dns.BADNAME`: 未格式化主机名
*   `dns.BADFAMILY`: 没有提供地址族
*   `dns.BADRESP`: 未格式化DNS回复
*   `dns.CONNREFUSED`: 无法连接DNS服务器
*   `dns.TIMEOUT`: 连接DNS服务器超时
*   `dns.EOF`: 文件末尾
*   `dns.FILE`: 读取文件错误
*   `dns.NOMEM`: 内存溢出
*   `dns.DESTRUCTION`: 通道以及销毁
*   `dns.BADSTR`: 未格式化字符串
*   `dns.BADFLAGS`: 指定非法标记
*   `dns.NONAME`: 给定的主机名不是数字。
*   `dns.BADHINTS`: 指定非法的提示标志。
*   `dns.NOTINITIALIZED`: `c-ares`异步DNS请求库初始化未完成。
*   `dns.LOADIPHLPAPI`: 加载`iphlpapi.dll`(Windows IP辅助API应用程序接口模块)错误
*   `dns.ADDRGETNETWORKPARAMS`: 找不到`GetNetworkParams`(读取本机DNS信息)函数
*   `dns.CANCELLED`: DNS查询取消
