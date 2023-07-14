# Lua 环境

您编写的 Lua 脚本将在 VLEGEND 的特定 Lua 运行环境中运行。
这个环境是沙盒化的，因此它与直接在命令行中运行 Lua 脚本会有一些不同。
这主要是因为在沙盒环境中，我们可以对脚本的运行环境进行更多的控制和约束，以增强安全性和稳定性。

目前我们的运行环境使用的是 [Lua 5.4](https://www.lua.org/manual/5.4/)，一个非常强大且灵活的嵌入式编程语言。

## 某些基础函数的限制

在 VLEGEND 的 Lua 运行环境中，部分基础函数是不可用的。这些包括：
- [dofile](https://www.lua.org/manual/5.4/manual.html#pdf-dofile)：在 Lua 环境中运行一个文件
- [load](https://www.lua.org/manual/5.4/manual.html#pdf-load)：动态加载 Lua 代码
- [loadfile](https://www.lua.org/manual/5.4/manual.html#pdf-loadfile)：加载并运行 Lua 文件
- [print](https://www.lua.org/manual/5.4/manual.html#pdf-print)：在控制台打印文本

为了替代 `print`，您可以使用 [`logging`](../api/logs.md) 模块来记录和查看运行日志。

## 可用的 Lua 标准库

虽然有一些 Lua 库无法在 VLEGEND 的环境中使用，但我们仍提供了一些基础且实用的 Lua 标准库供您使用。以下是当前环境中可用的标准库：
- [coroutine](https://www.lua.org/manual/5.4/manual.html#6.2)：提供对协程的支持，以实现复杂的控制流
- [string](https://www.lua.org/manual/5.4/manual.html#6.4)：对字符串操作的功能，如查找，替换，模式匹配等
- [utf8](https://www.lua.org/manual/5.4/manual.html#6.5)：对 UTF-8 编码字符串的操作功能
- [table](https://www.lua.org/manual/5.4/manual.html#6.6)：Lua 的关联数组实现，提供了一系列操作和管理表的功能
- [math](https://www.lua.org/manual/5.4/manual.html#6.7)：提供一套广泛的数学函数和常数

这些库可以帮助您快速实现各种功能，使您的脚本更强大，更高效。

## 标准库增强

标准库中的部分方法被替换为 Rust 版本，它们的行为可能发生变化，请注意。

### math.random([m [, n]])

random 方法被替换为了 Rust 实现并提供真随机数（CSPRNG），不再需要调用 `math.randomseed` 进行初始化。

若要填入参数，则 `m` 和 `n` 均为整数。

- 无参调用时，返回 [0, 1] 的浮点数。
- `math.random(0)` 返回一个完全随机的整数。
- `math.random(n)` 返回 [1, n] 之间的整数，`n` 需要为正整数。
- `math.random(m, n)` 返回 [n, m] 之间的整数，`m` 必须小于 `n`。