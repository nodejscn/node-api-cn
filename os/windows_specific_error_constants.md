
The following error codes are specific to the Windows operating system:

<table>
  <tr>
    <th>Constant</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>WSAEINTR</code></td>
    <td>Indicates an interrupted function call.</td>
  </tr>
  <tr>
    <td><code>WSAEBADF</code></td>
    <td>Indicates an invalid file handle.</td>
  </tr>
  <tr>
    <td><code>WSAEACCES</code></td>
    <td>Indicates insufficient permissions to complete the operation.</td>
  </tr>
  <tr>
    <td><code>WSAEFAULT</code></td>
    <td>Indicates an invalid pointer address.</td>
  </tr>
  <tr>
    <td><code>WSAEINVAL</code></td>
    <td>Indicates that an invalid argument was passed.</td>
  </tr>
  <tr>
    <td><code>WSAEMFILE</code></td>
    <td>Indicates that there are too many open files.</td>
  </tr>
  <tr>
    <td><code>WSAEWOULDBLOCK</code></td>
    <td>Indicates that a resource is temporarily unavailable.</td>
  </tr>
  <tr>
    <td><code>WSAEINPROGRESS</code></td>
    <td>Indicates that an operation is currently in progress.</td>
  </tr>
  <tr>
    <td><code>WSAEALREADY</code></td>
    <td>Indicates that an operation is already in progress.</td>
  </tr>
  <tr>
    <td><code>WSAENOTSOCK</code></td>
    <td>Indicates that the resource is not a socket.</td>
  </tr>
  <tr>
    <td><code>WSAEDESTADDRREQ</code></td>
    <td>Indicates that a destination address is required.</td>
  </tr>
  <tr>
    <td><code>WSAEMSGSIZE</code></td>
    <td>Indicates that the message size is too long.</td>
  </tr>
  <tr>
    <td><code>WSAEPROTOTYPE</code></td>
    <td>Indicates the wrong protocol type for the socket.</td>
  </tr>
  <tr>
    <td><code>WSAENOPROTOOPT</code></td>
    <td>Indicates a bad protocol option.</td>
  </tr>
  <tr>
    <td><code>WSAEPROTONOSUPPORT</code></td>
    <td>Indicates that the protocol is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAESOCKTNOSUPPORT</code></td>
    <td>Indicates that the socket type is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEOPNOTSUPP</code></td>
    <td>Indicates that the operation is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEPFNOSUPPORT</code></td>
    <td>Indicates that the protocol family is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEAFNOSUPPORT</code></td>
    <td>Indicates that the address family is not supported.</td>
  </tr>
  <tr>
    <td><code>WSAEADDRINUSE</code></td>
    <td>Indicates that the network address is already in use.</td>
  </tr>
  <tr>
    <td><code>WSAEADDRNOTAVAIL</code></td>
    <td>Indicates that the network address is not available.</td>
  </tr>
  <tr>
    <td><code>WSAENETDOWN</code></td>
    <td>Indicates that the network is down.</td>
  </tr>
  <tr>
    <td><code>WSAENETUNREACH</code></td>
    <td>Indicates that the network is unreachable.</td>
  </tr>
  <tr>
    <td><code>WSAENETRESET</code></td>
    <td>Indicates that the network connection has been reset.</td>
  </tr>
  <tr>
    <td><code>WSAECONNABORTED</code></td>
    <td>Indicates that the connection has been aborted.</td>
  </tr>
  <tr>
    <td><code>WSAECONNRESET</code></td>
    <td>Indicates that the connection has been reset by the peer.</td>
  </tr>
  <tr>
    <td><code>WSAENOBUFS</code></td>
    <td>Indicates that there is no buffer space available.</td>
  </tr>
  <tr>
    <td><code>WSAEISCONN</code></td>
    <td>Indicates that the socket is already connected.</td>
  </tr>
  <tr>
    <td><code>WSAENOTCONN</code></td>
    <td>Indicates that the socket is not connected.</td>
  </tr>
  <tr>
    <td><code>WSAESHUTDOWN</code></td>
    <td>Indicates that data cannot be sent after the socket has been
    shutdown.</td>
  </tr>
  <tr>
    <td><code>WSAETOOMANYREFS</code></td>
    <td>Indicates that there are too many references.</td>
  </tr>
  <tr>
    <td><code>WSAETIMEDOUT</code></td>
    <td>Indicates that the connection has timed out.</td>
  </tr>
  <tr>
    <td><code>WSAECONNREFUSED</code></td>
    <td>Indicates that the connection has been refused.</td>
  </tr>
  <tr>
    <td><code>WSAELOOP</code></td>
    <td>Indicates that a name cannot be translated.</td>
  </tr>
  <tr>
    <td><code>WSAENAMETOOLONG</code></td>
    <td>Indicates that a name was too long.</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTDOWN</code></td>
    <td>Indicates that a network host is down.</td>
  </tr>
  <tr>
    <td><code>WSAEHOSTUNREACH</code></td>
    <td>Indicates that there is no route to a network host.</td>
  </tr>
  <tr>
    <td><code>WSAENOTEMPTY</code></td>
    <td>Indicates that the directory is not empty.</td>
  </tr>
  <tr>
    <td><code>WSAEPROCLIM</code></td>
    <td>Indicates that there are too many processes.</td>
  </tr>
  <tr>
    <td><code>WSAEUSERS</code></td>
    <td>Indicates that the user quota has been exceeded.</td>
  </tr>
  <tr>
    <td><code>WSAEDQUOT</code></td>
    <td>Indicates that the disk quota has been exceeded.</td>
  </tr>
  <tr>
    <td><code>WSAESTALE</code></td>
    <td>Indicates a stale file handle reference.</td>
  </tr>
  <tr>
    <td><code>WSAEREMOTE</code></td>
    <td>Indicates that the item is remote.</td>
  </tr>
  <tr>
    <td><code>WSASYSNOTREADY</code></td>
    <td>Indicates that the network subsystem is not ready.</td>
  </tr>
  <tr>
    <td><code>WSAVERNOTSUPPORTED</code></td>
    <td>Indicates that the winsock.dll version is out of range.</td>
  </tr>
  <tr>
    <td><code>WSANOTINITIALISED</code></td>
    <td>Indicates that successful WSAStartup has not yet been performed.</td>
  </tr>
  <tr>
    <td><code>WSAEDISCON</code></td>
    <td>Indicates that a graceful shutdown is in progress.</td>
  </tr>
  <tr>
    <td><code>WSAENOMORE</code></td>
    <td>Indicates that there are no more results.</td>
  </tr>
  <tr>
    <td><code>WSAECANCELLED</code></td>
    <td>Indicates that an operation has been canceled.</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROCTABLE</code></td>
    <td>Indicates that the procedure call table is invalid.</td>
  </tr>
  <tr>
    <td><code>WSAEINVALIDPROVIDER</code></td>
    <td>Indicates an invalid service provider.</td>
  </tr>
  <tr>
    <td><code>WSAEPROVIDERFAILEDINIT</code></td>
    <td>Indicates that the service provider failed to initialized.</td>
  </tr>
  <tr>
    <td><code>WSASYSCALLFAILURE</code></td>
    <td>Indicates a system call failure.</td>
  </tr>
  <tr>
    <td><code>WSASERVICE_NOT_FOUND</code></td>
    <td>Indicates that a service was not found.</td>
  </tr>
  <tr>
    <td><code>WSATYPE_NOT_FOUND</code></td>
    <td>Indicates that a class type was not found.</td>
  </tr>
  <tr>
    <td><code>WSA_E_NO_MORE</code></td>
    <td>Indicates that there are no more results.</td>
  </tr>
  <tr>
    <td><code>WSA_E_CANCELLED</code></td>
    <td>Indicates that the call was canceled.</td>
  </tr>
  <tr>
    <td><code>WSAEREFUSED</code></td>
    <td>Indicates that a database query was refused.</td>
  </tr>
</table>

