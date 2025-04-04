## 什么是 Node.js 中的事件循环？
> 八股文一网打尽，更多面试题请看[程序员面试刷题神器 - 面试鸭](https://www.mianshiya.com/)

## 回答重点
Node.js 中的事件循环是一个核心概念，它是 Node.js 处理异步操作的基础。简而言之，事件循环是一个永远运行的循环，它使得 Node.js 能够非阻塞地执行 I/O 操作，即使在执行其他操作时也能继续处理新的请求。

在 Node.js 中，事件循环分为几个阶段，每个阶段都有不同类型的操作，Node.js 会在每个阶段处理相应的回调函数。这些阶段按照一个固定的顺序执行，确保了异步操作按预期进行。

## 扩展知识
既然我们了解了事件循环的基本知识，我可以进一步解释一下事件循环的各个阶段和它们的作用，以帮助你更好地理解这个概念。

1）**Timers（定时器阶段）**：这个阶段主要处理 `setTimeout` 和 `setInterval` 的回调函数。如果有到期的定时器，它们的回调函数将在这个阶段执行。

2）**I/O callbacks（I/O 回调阶段）**：这个阶段处理几乎所有的回调，除了 `close` 事件的回调、阻塞操作的回调等。

3）**idle, prepare（空闲、准备阶段）**：这是 Node.js 内部使用的一个阶段，通常不对用户公开。

4）**poll（轮询阶段）**：这个阶段主要负责查看是否有 I/O 需要处理，如果有则处理它们，如果没有则会适当地休眠等待任务。

5）**check（检查阶段）**：这个阶段专门用于执行 `setImmediate` 回调，这是一个立刻执行的机制，不会等待下一个循环。

6）**close callbacks（关闭回调阶段）**：这个阶段用来处理如 `socket.on('close', ...)` 的回调。

在了解了这些阶段之后，你会发现 Node.js 之所以能够高效处理并行的 I/O 操作，正是因为它运用了这种事件驱动的机制。事件循环不断地检查和执行各种回调，使得即使一个操作在等待 I/O 或其他异步任务时，服务器也不会被阻塞。

为了加深理解，你可以尝试写一些简单的例子，例如设置多个 `setTimeout`、使用 `setImmediate` 等等，并观察它们的执行顺序。



> 八股文一网打尽，更多面试题请看[程序员面试刷题神器 - 面试鸭](https://www.mianshiya.com/)