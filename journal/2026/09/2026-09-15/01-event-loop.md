# asyncio 事件循环的运行机制

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程 · 第 1 则

## 学习目标

搞清楚事件循环在整个异步模型中的角色，理解它为什么是 asyncio 的核心。

## 核心要点

- 事件循环负责调度协程、回调、定时器与 IO 事件，是单线程内实现并发的引擎。
- asyncio.run() 会创建新的循环并在结束后关闭，嵌套调用会抛出 RuntimeError。
- loop.run_until_complete() 是旧式入口，新代码应优先使用 asyncio.run()。

## 示例

```python
import asyncio

async def main():
    print("loop:", asyncio.get_running_loop())

asyncio.run(main())
```

## 易错点

- 在协程内部直接调用 asyncio.get_event_loop() 容易拿到已关闭的循环，改用 get_running_loop() 更安全。

## 小结

事件循环是调度中枢，理解它的生命周期是排查异步问题的第一步。
