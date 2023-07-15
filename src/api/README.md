# API

本节列出了所有你可以使用的 API。

你可能已经注意到，部分 API 以 `Action` 或者 `Actions` 结尾。
这表明这些 API 的调用会产生事件，在使用这些 API 的时候，你应当将产生的事件返回给引擎。

`Action` 代表该 API 会产生一个事件，它的返回值是 [`Event`](./event.md#event)。
`Actions` 代表该 API 可能会产生复数个事件，它的返回值是一个 [`Event`](./event.md#event) 的数组。