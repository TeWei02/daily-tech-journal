# 用 Semaphore 限制并发数量

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程 · 第 5 则

## 学习目标

在批量请求场景下控制同时打开的任务数，避免打爆下游服务。

## 核心要点

- Semaphore 内部维护计数器，acquire 减一、release 加一，计数为零时后续任务排队等待。
- 推荐用 async with 语法，保证异常路径下也能正确释放。
- 并发上限应结合下游限流、本机连接数与内存实际情况设定。

## 示例

```python
sem = asyncio.Semaphore(5)

async def worker(i):
    async with sem:
        await asyncio.sleep(0.1)
        return i
```

## 易错点

- 直接 acquire 而不用上下文管理器，一旦中途异常就会永久占用信号量。

## 小结

Semaphore 是异步场景下最轻量的限流手段。
