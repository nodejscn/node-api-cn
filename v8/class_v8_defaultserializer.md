<!--
added: v8.0.0
-->

A subclass of [`Serializer`][] that serializes `TypedArray`
(in particular [`Buffer`][]) and `DataView` objects as host objects, and only
stores the part of their underlying `ArrayBuffer`s that they are referring to.

