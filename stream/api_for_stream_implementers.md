
<!--type=misc-->

The `stream` module API has been designed to make it possible to easily
implement streams using JavaScript's prototypal inheritance model.

First, a stream developer would declare a new JavaScript class that extends one
of the four basic stream classes (`stream.Writable`, `stream.Readable`,
`stream.Duplex`, or `stream.Transform`), making sure they call the appropriate
parent class constructor:

```js
const { Writable } = require('stream');

class MyWritable extends Writable {
  constructor(options) {
    super(options);
    // ...
  }
}
```

The new stream class must then implement one or more specific methods, depending
on the type of stream being created, as detailed in the chart below:

<table>
  <thead>
    <tr>
      <th>
        <p>Use-case</p>
      </th>
      <th>
        <p>Class</p>
      </th>
      <th>
        <p>Method(s) to implement</p>
      </th>
    </tr>
  </thead>
  <tr>
    <td>
      <p>Reading only</p>
    </td>
    <td>
      <p>[Readable](#stream_class_stream_readable)</p>
    </td>
    <td>
      <p><code>[_read][stream-_read]</code></p>
    </td>
  </tr>
  <tr>
    <td>
      <p>Writing only</p>
    </td>
    <td>
      <p>[Writable](#stream_class_stream_writable)</p>
    </td>
    <td>
      <p><code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>,
      <code>[_final][stream-_final]</code></p>
    </td>
  </tr>
  <tr>
    <td>
      <p>Reading and writing</p>
    </td>
    <td>
      <p>[Duplex](#stream_class_stream_duplex)</p>
    </td>
    <td>
      <p><code>[_read][stream-_read]</code>, <code>[_write][stream-_write]</code>, <code>[_writev][stream-_writev]</code>,
      <code>[_final][stream-_final]</code></p>
    </td>
  </tr>
  <tr>
    <td>
      <p>Operate on written data, then read the result</p>
    </td>
    <td>
      <p>[Transform](#stream_class_stream_transform)</p>
    </td>
    <td>
      <p><code>[_transform][stream-_transform]</code>, <code>[_flush][stream-_flush]</code>,
      <code>[_final][stream-_final]</code></p>
    </td>
  </tr>
</table>

*Note*: The implementation code for a stream should *never* call the "public"
methods of a stream that are intended for use by consumers (as described in
the [API for Stream Consumers][] section). Doing so may lead to adverse
side effects in application code consuming the stream.

