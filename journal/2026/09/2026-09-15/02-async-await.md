# async/await 语法与协程对象

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程

## 一句话说明

区分协程函数与协程对象，明确 await 的实际语义。

## 关键点

- async def 定义的是协程函数，调用后返回协程对象，此时函数体并未执行。
- await 只能出现在 async 函数中，用于等待另一个 awaitable 并把控制权交还事件循环。
- 忘记 await 会得到 "coroutine was never awaited" 警告，且逻辑不会执行。

## 代码 / 命令

```python
async def fetch():
    await asyncio.sleep(1)
    return 42

result = asyncio.run(fetch())
print(result)
```

## 注意事项

- 把协程对象直接放进列表推导式而不 await，会静默地什么都不做。

## 小结

协程是惰性的，只有被 await 或被封装成 Task 才会真正运行。
