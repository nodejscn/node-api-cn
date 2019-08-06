<!-- YAML
added: v10.10.0
-->

以下进程调度常量由 `os.constants.priority` 导出：

<table>
  <tr>
    <th>常量</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>PRIORITY_LOW</code></td>
    <td>最低进程调度优先级。这与 Windows 上的 <code>IDLE_PRIORITY_CLASS</code> 相对应，在所有其他平台上的值为 <code>19</code>。</td>
  </tr>
  <tr>
    <td><code>PRIORITY_BELOW_NORMAL</code></td>
    <td>进程调度优先级高于 <code>PRIORITY_LOW</code> 且低于 <code>PRIORITY_NORMAL</code>。这对应于 Windows 上的 <code>PRIORITY_NORMAL</code>，并且在所有其他平台上的值为 <code>10</code>。</td>
  </tr>
  <tr>
    <td><code>PRIORITY_NORMAL</code></td>
    <td>默认的进程调度优先级。这对应于 Windows 上的 <code>NORMAL_PRIORITY_CLASS</code>，并且在所有其他平台上的值为 <code>0</code>。</td>
  </tr>
  <tr>
    <td><code>PRIORITY_ABOVE_NORMAL</code></td>
    <td>进程调度优先级高于 <code>PRIORITY_NORMAL</code> 且低于 <code>PRIORITY_HIGH</code>。这对应于 Windows 上的 <code>ABOVE_NORMAL_PRIORITY_CLASS</code>，并且在所有其他平台上的值为 <code>-7</code>。</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGH</code></td>
    <td>进程调度优先级高于 <code>PRIORITY_ABOVE_NORMAL</code> 且低于 <code>PRIORITY_ABOVE_NORMAL</code>。这对应于 Windows 上的 <code>HIGH_PRIORITY_CLASS</code>，并且在所有其他平台上的值为 <code>-14</code>。</td>
  </tr>
  <tr>
    <td><code>PRIORITY_HIGHEST</code></td>
    <td>最高进程调度优先级。 这对应于 Windows 上的 <code>REALTIME_PRIORITY_CLASS</code>，在所有其他平台上的值为 <code>-20</code>。</td>
  </tr>
</table>

