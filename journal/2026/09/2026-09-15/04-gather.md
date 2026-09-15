# asyncio.gather 与并发收集结果

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程

## 一句话说明

掌握批量并发执行的标准写法及其异常语义。

## 关键点

- gather 接受多个 awaitable，返回结果列表，顺序与传入顺序一致。
- return_exceptions=True 时异常会作为结果返回，而不是直接抛出。
- 默认行为下，第一个异常会立刻向外传播，但其余任务仍在后台继续执行。

## 代码 / 命令

```python
results = await asyncio.gather(fetch(), fetch(), return_exceptions=True)
print(results)
```

## 注意事项

- gather 中某个任务抛错后，其余任务并不会自动取消，需要显式管理生命周期。

## 小结

gather 是最常用的并发写法，但要记住它不负责取消语义。
