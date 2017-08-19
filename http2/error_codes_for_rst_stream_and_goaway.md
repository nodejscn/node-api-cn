<a id="error_codes"></a>

| Value | Name                | Constant                                      |
|-------|---------------------|-----------------------------------------------|
| 0x00  | No Error            | `http2.constants.NGHTTP2_NO_ERROR`            |
| 0x01  | Protocol Error      | `http2.constants.NGHTTP2_PROTOCOL_ERROR`      |
| 0x02  | Internal Error      | `http2.constants.NGHTTP2_INTERNAL_ERROR`      |
| 0x03  | Flow Control Error  | `http2.constants.NGHTTP2_FLOW_CONTROL_ERROR`  |
| 0x04  | Settings Timeout    | `http2.constants.NGHTTP2_SETTINGS_TIMEOUT`    |
| 0x05  | Stream Closed       | `http2.constants.NGHTTP2_STREAM_CLOSED`       |
| 0x06  | Frame Size Error    | `http2.constants.NGHTTP2_FRAME_SIZE_ERROR`    |
| 0x07  | Refused Stream      | `http2.constants.NGHTTP2_REFUSED_STREAM`      |
| 0x08  | Cancel              | `http2.constants.NGHTTP2_CANCEL`              |
| 0x09  | Compression Error   | `http2.constants.NGHTTP2_COMPRESSION_ERROR`   |
| 0x0a  | Connect Error       | `http2.constants.NGHTTP2_CONNECT_ERROR`       |
| 0x0b  | Enhance Your Calm   | `http2.constants.NGHTTP2_ENHANCE_YOUR_CALM`   |
| 0x0c  | Inadequate Security | `http2.constants.NGHTTP2_INADEQUATE_SECURITY` |
| 0x0d  | HTTP/1.1 Required   | `http2.constants.NGHTTP2_HTTP_1_1_REQUIRED`   |

The `'timeout'` event is emitted when there is no activity on the Server for
a given number of milliseconds set using `http2server.setTimeout()`.

