
以下常量用于 `fs.open()`。

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>O_RDONLY</code></td>
    <td>表明打开文件用于只读访问。</td>
  </tr>
  <tr>
    <td><code>O_WRONLY</code></td>
    <td>表明打开文件用于只写访问。</td>
  </tr>
  <tr>
    <td><code>O_RDWR</code></td>
    <td>表明打开文件用于读写访问。</td>
  </tr>
  <tr>
    <td><code>O_CREAT</code></td>
    <td>表明如果文件不存在则创建文件。</td>
  </tr>
  <tr>
    <td><code>O_EXCL</code></td>
    <td>表明如果设置了 <code>O_CREAT</code> 标志且文件已存在，则打开文件时会失败。</td>
  </tr>
  <tr>
    <td><code>O_NOCTTY</code></td>
    <td>表明如果路径是一个终端设备，则打开该路径不应该造成该终端变成进程的控制终端（如果进程还没有终端）。</td>
  </tr>
  <tr>
    <td><code>O_TRUNC</code></td>
    <td>表明如果文件已存在且为一个普通文件、且文件被成功打开为写入访问，则它的长度会被截断至零。</td>
  </tr>
  <tr>
    <td><code>O_APPEND</code></td>
    <td>表明数据会被追加到文件的末尾。</td>
  </tr>
  <tr>
    <td><code>O_DIRECTORY</code></td>
    <td>表明如果路径不是一个目录，则打开会失败。</td>
  </tr>
  <tr>
  <td><code>O_NOATIME</code></td>
    <td>表明文件系统的读取访问不再引起文件的 <code>atime</code> 信息的更新。
    只在 Linux 操作系统有效。</td>
  </tr>
  <tr>
    <td><code>O_NOFOLLOW</code></td>
    <td>表明如果路径是一个符号链接，则打开会失败。</td>
  </tr>
  <tr>
    <td><code>O_SYNC</code></td>
    <td>表明文件以同步 I/O 打开，写入操作会等待文件的完整性。</td>
  </tr>
  <tr>
    <td><code>O_DSYNC</code></td>
    <td>表明文件以同步 I/O 打开，写入操作会等待数据的完整性</td>
  </tr>
  <tr>
    <td><code>O_SYMLINK</code></td>
    <td>表明打开符号链接自身，而不是它指向的资源。</td>
  </tr>
  <tr>
    <td><code>O_DIRECT</code></td>
    <td>表明会尝试最小化文件 I/O 的缓存效果。</td>
  </tr>
  <tr>
    <td><code>O_NONBLOCK</code></td>
    <td>表明以非阻塞模式打开文件。</td>
  </tr>
</table>

