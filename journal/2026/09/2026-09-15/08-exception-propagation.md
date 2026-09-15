# 异常传播与后台任务告警

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程

## 一句话说明

搞清楚异常在 Task 与 gather 之间如何流动。

## 关键点

- Task 中的未捕获异常会在 await 时重新抛出。
- 从未被 await 的 Task 异常会在垃圾回收时打印警告日志。
- 生产代码应统一在任务入口捕获异常并记录，避免静默失败。

## 代码 / 命令

```python
task = asyncio.create_task(risky())
task.add_done_callback(lambda t: print(t.exception()))
```

## 注意事项

- 仅用 create_task 而不管返回值，是异步代码里最常见的静默失败来源。

## 小结

后台任务必须有人负责兜住异常。
