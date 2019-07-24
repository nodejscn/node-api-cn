下面的错误码与Windows系统相关:

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>WSAEINTR</code></td>
    <td>表明中断的函数调用 .</td>
  </tr>
  <tr>
    <td><code>WSAEBADF</code></td>
    <td>表明一个无效的文件句柄 .</td>
  </tr>
  <tr>
    <td><code>WSAEACCES</code></td>
    <td>表明权限不够完成操作 .</td>
  </tr>
  <tr>
    <td><code>WSAEFAULT</code></td>
    <td>表明无效的指针地址 .</td>
  </tr>
  <tr>
    <td><code>WSAEINVAL</code></td>
    <td>表明无效的参数被传递 .</td>
  </tr>
  <tr>
    <td><code>WSAEMFILE</code></td>
    <td>表明有太多打开的文件 .</td>
  </tr>
  <tr>
    <td><code>WSAEWOULDBLOCK</code></td>
    <td>表明资源暂时不可用 .</td>
  </tr>
  <tr>
    <td><code>WSAEINPROGRESS</code></td>
    <td>表明操作当前正在进行中 .</td>
  </tr>
  <tr>
    <td><code>WSAEALREADY</code></td>
    <td>表明操作已经在进行中 .</td>
  </tr>
  <tr>
    <td><code>WSAENOTSOCK</code></td>
    <td>表明资源不是 socket.</td>
  </tr>
  <tr>
    <td><code>WSAEDESTADDRREQ</code></td>
    <td>表明需要目的地址 .</td>
  </tr>
  <tr>
    <td><code>WSAEMSGSIZE</code></td>
    <td>表明消息太长 .</td>
  </tr>
  <tr>
    <td><code>WSAEPROTOTYPE</code></td>
    <td>表明socket协议类型错误 .</td>
  </tr>
  <tr>
    <td><code>WSAENOPROTOOPT</code></td>
    <td>表明错误的协议选项 .</td>
  </tr>
  <tr>
    <td><code>WSAEPROTONOSUPPORT</code></td>
    <td>表明协议不被支持 .</td>
  </tr>
  <tr>
    <td><code>WSAESOCKTNOSUPPORT</code></td>
    <td>表明socket类型不被支持 .</td>
  </tr>
  <tr>
    <td><code>WSAEOPNOTSUPP</code></td>
    <td>表明操作不被支持 .</td>
  </tr>
  <tr>
    <td><code>WSAEPFNOSUPPORT</code></td>
    <td>表明协议簇不被支持 .</td>
  </tr>
  <tr>
    <td><code>WSAEAFNOSUPPORT</code></td>
    <td>表明地址簇不被支持 .</td>
  </tr>
  <tr>
    <td><code>WSAEADDRINUSE</code></td>
    <td>表明网络地址已经在使用 .</td>
  </tr>
  <tr>
    <td><code>WSAEADDRNOTAVAIL</code></td>
    <td>表明网络地址不可用.</td>
  </tr>
  <tr>
    <td><code>WSAENETDOWN</code></td>
    <td>表明网络关闭 .</td>
  </tr>
  <tr>
    <td><code>WSAENETUNREACH</code></td>
    <td>表明网络不可达 .</td>
  </tr>
  <tr>
    <td><code>WSAENETRESET</code></td>
    <td>表明网络连接被重置 .</td>
  </tr>
  <tr>
    <td><code>WSAECONNABORTED</code></td>
    <td>表明连接被终止 .</td>
  </tr>
  <tr>
    <td><code>WSAECONNRESET</code></td>
    <td>表明连接被同伴重置 .</td>
  </tr>
  <tr>
    <td><code>WSAENOBUFS</code></td>
    <td>表明没有可用的缓存空间 .</td>
  </tr>
  <tr>
    <td><code>WSAEISCONN</code></td>
    <td>表明socket已经连接 .</td>
  </tr>
  <tr>
    <td><code>WSAENOTCONN</code></td>
    <td>表明socket没有连接 .</td>
  </tr>
  <tr>
    <td><code>WSAESHUTDOWN</code></td>
    <td>表明数据在socket关闭之后,不能被发送 .</td>
  </tr>
  <tr>
    <td><code>WSAETOOMANYREFS</code></td>
    <td>表明有太多的引用 .</td>
  </tr>
  <tr>
    <td><code>WSAETIMEDOUT</code></td>
    <td>表明连接超时 .</td>
  </tr>
  <tr>
    <td><code>WSAECONNREFUSED</code></td>
    <td>表明连接被拒绝 .</td>
  </tr>
  <tr>
    <td><code>WSAELOOP</code></td>
    <td>表明名字不能被翻译 .</td>
  </tr>
  <tr>
    <td><code>WSAENAMETOOLONG</code></td>
    <td>表明名字太长 .</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTDOWN</code></td>
    <td>表明网络主机关闭 .</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTUNREACH</code></td>
    <td>表明没有到网络主机的路由 .</td>
  </tr>
  <tr>
    <td><code>WSAENOTEMPTY</code></td>
    <td>表明目录非空 .</td>
  </tr>
  <tr>
    <td><code>WSAEPROCLIM</code></td>
    <td>表明有太多的进程 .</td>
  </tr>
  <tr>
    <td><code>WSAEUSERS</code></td>
    <td>表明已经超过用户指标 .</td>
  </tr>
  <tr>
    <td><code>WSAEDQUOT</code></td>
    <td>表明已经超过磁盘指标 .</td>
  </tr>
  <tr>
    <td><code>WSAESTALE</code></td>
    <td>表明一个稳定的文件句柄引用 .</td>
  </tr>
  <tr>
    <td><code>WSAEREMOTE</code></td>
    <td>表明项目是远程的 .</td>
  </tr>
  <tr>
    <td><code>WSASYSNOTREADY</code></td>
    <td>表明网络子系统尚未准备好 .</td>
  </tr>
  <tr>
    <td><code>WSAVERNOTSUPPORTED</code></td>
    <td>表明 winsock.dll 版本在范围之外.</td>
  </tr>
  <tr>
    <td><code>WSANOTINITIALISED</code></td>
    <td>表明成功的 WSAStartup(Windows异步socket)还没有被执行 .</td>
  </tr>
  <tr>
    <td><code>WSAEDISCON</code></td>
    <td>表明一个优雅的关机正在进行 .</td>
  </tr>
  <tr>
    <td><code>WSAENOMORE</code></td>
    <td>表明没有更多的结果 .</td>
  </tr>
  <tr>
    <td><code>WSAECANCELLED</code></td>
    <td>表明一个操作已经被取消 .</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROCTABLE</code></td>
    <td>表明过程调用表是无效的 .</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROVIDER</code></td>
    <td>表明无效的服务提供者 .</td>
  </tr>
  <tr>
    <td><code>WSAEPROVIDERFAILEDINIT</code></td>
    <td>表明服务提供者初始化失败 .</td>
  </tr>
  <tr>
    <td><code>WSASYSCALLFAILURE</code></td>
    <td>表明系统调用失败 .</td>
  </tr>
  <tr>
    <td><code>WSASERVICE_NOT_FOUND</code></td>
    <td>表明服务没有被找到 .</td>
  </tr>
  <tr>
    <td><code>WSATYPE_NOT_FOUND</code></td>
    <td>表明类类型没有被找到 .</td>
  </tr>
  <tr>
    <td><code>WSA_E_NO_MORE</code></td>
    <td>表明没有更多的结果 .</td>
  </tr>
  <tr>
    <td><code>WSA_E_CANCELLED</code></td>
    <td>表明调用被取消 .</td>
  </tr>
  <tr>
    <td><code>WSAEREFUSED</code></td>
    <td>表明数据库请求被拒绝 .</td>
  </tr>
</table>

