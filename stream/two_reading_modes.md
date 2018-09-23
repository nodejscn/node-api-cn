
`Readable` streams effectively operate in one of two modes: flowing and
paused. These modes are separate from [object mode][object-mode].
A [`Readable`][] stream can be in object mode or not, regardless of whether
it is in flowing mode or paused mode.

* In flowing mode, data is read from the underlying system automatically
and provided to an application as quickly as possible using events via the
[`EventEmitter`][] interface.

* In paused mode, the [`stream.read()`][stream-read] method must be called
explicitly to read chunks of data from the stream.

All [`Readable`][] streams begin in paused mode but can be switched to flowing
mode in one of the following ways:

* Adding a [`'data'`][] event handler.
* Calling the [`stream.resume()`][stream-resume] method.
* Calling the [`stream.pipe()`][] method to send the data to a [`Writable`][].

The `Readable` can switch back to paused mode using one of the following:

* If there are no pipe destinations, by calling the
  [`stream.pause()`][stream-pause] method.
* If there are pipe destinations, by removing all pipe destinations.
  Multiple pipe destinations may be removed by calling the
  [`stream.unpipe()`][] method.

The important concept to remember is that a `Readable` will not generate data
until a mechanism for either consuming or ignoring that data is provided. If
the consuming mechanism is disabled or taken away, the `Readable` will *attempt*
to stop generating the data.

For backwards compatibility reasons, removing [`'data'`][] event handlers will
**not** automatically pause the stream. Also, if there are piped destinations,
then calling [`stream.pause()`][stream-pause] will not guarantee that the
stream will *remain* paused once those destinations drain and ask for more data.

If a [`Readable`][] is switched into flowing mode and there are no consumers
available to handle the data, that data will be lost. This can occur, for
instance, when the `readable.resume()` method is called without a listener
attached to the `'data'` event, or when a `'data'` event handler is removed
from the stream.

Adding a [`'readable'`][] event handler automatically make the stream to
stop flowing, and the data to be consumed via
[`readable.read()`][stream-read]. If the [`'readable'`] event handler is
removed, then the stream will start flowing again if there is a
[`'data'`][] event handler.

