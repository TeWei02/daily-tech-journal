# 超时与任务取消处理

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程 · 第 7 则

## 学习目标

给异步任务加上可靠的时间边界，并正确处理取消信号。

## 核心要点

- asyncio.wait_for 会为等待设置超时，超时后抛出 TimeoutError 并尝试取消任务。
- Python 3.11 起可用 asyncio.timeout 上下文管理器，代码更直观。
- 协程收到取消时会抛 CancelledError，通常应让它继续向外传播。

## 示例

```python
try:
    await asyncio.wait_for(fetch(), timeout=2)
except asyncio.TimeoutError:
    print("timeout")
```

## 易错点

- 用裸 except 吞掉 CancelledError 会破坏取消机制，导致任务无法退出。

## 小结

超时与取消是异步健壮性的基础，不要静默吞掉取消异常。
