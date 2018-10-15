
可读流的 API 贯穿了多个 Node.js 版本，且提供了多种方法来消费流数据。
开发者通常应该选择其中一种方法来消费数据，不要在单个流使用多种方法来消费数据。
混合使用 `on('data')`、`on('readable')`、`pipe()` 或异步迭代器，会导致不明确的行为。

对于大多数用户，建议使用 `readable.pipe()`，因为它是消费流数据最简单的方式。
如果开发者需要精细地控制数据的传递与产生，可以使用 [`EventEmitter`]、`readable.on('readable')`/`readable.read()` 或 `readable.pause()`/`readable.resume()`。

