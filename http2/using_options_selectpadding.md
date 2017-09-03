
When `options.paddingStrategy` is equal to
`http2.constants.PADDING_STRATEGY_CALLBACK`, the the HTTP/2 implementation will
consult the `options.selectPadding` callback function, if provided, to determine
the specific amount of padding to use per HEADERS and DATA frame.

The `options.selectPadding` function receives two numeric arguments,
`frameLen` and `maxFrameLen` and must return a number `N` such that
`frameLen <= N <= maxFrameLen`.

```js
const http2 = require('http2');
const server = http2.createServer({
  paddingStrategy: http2.constants.PADDING_STRATEGY_CALLBACK,
  selectPadding(frameLen, maxFrameLen) {
    return maxFrameLen;
  }
});
```

*Note*: The `options.selectPadding` function is invoked once for *every*
HEADERS and DATA frame. This has a definite noticeable impact on
performance.

