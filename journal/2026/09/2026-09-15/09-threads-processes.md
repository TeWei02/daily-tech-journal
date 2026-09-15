# 异步、线程与多进程的取舍

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程 · 第 9 则

## 学习目标

建立选择模型的判断依据。

## 核心要点

- IO 密集型任务用异步收益最大，因为等待期间可以切换任务。
- CPU 密集型任务受 GIL 限制，应使用多进程或将热点交给原生扩展。
- 已有同步阻塞库难以改造时，可以用线程池配合 run_in_executor 过渡。

## 示例

```python
loop = asyncio.get_running_loop()
result = await loop.run_in_executor(None, blocking_io)
```

## 易错点

- 把 CPU 密集计算直接写进协程，会让整个事件循环失去响应。

## 小结

先判断瓶颈类型，再决定并发模型。
