# async with 异步上下文管理器：并发与线程安全

**日期**：2026-08-31　**领域**：Python　**编号**：112/115

## 背景

共享可变状态是并发问题的根源，能消除就消除。这里围绕「async with 异步上下文管理器」做一次整理，重点放在能直接落地的部分。

## 要点

- __aenter__/__aexit__ 返回 awaitable，with 语法在协程中会退化为同步阻塞
- 异常传递路径与同步版本一致，__aexit__ 返回 True 可吞掉异常
- 并发缺陷难以复现，需靠压测与竞态注入暴露。

## 示例

```python
class Pool:
    async def __aenter__(self):
        self.conn = await connect()
        return self.conn

    async def __aexit__(self, *exc):
        await self.conn.close()
```

## 易错点

- 忘记 await 会得到协程对象本身，必须先 await 再进入 with

## 小结

async with 异步上下文管理器 在并发与线程安全这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
