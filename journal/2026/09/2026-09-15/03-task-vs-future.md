# Task 与 Future 的区别

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程 · 第 3 则

## 学习目标

弄清两者关系，知道什么时候该用哪一个。

## 核心要点

- Future 是一个占位容器，代表将来会有的结果，本身不承载逻辑。
- Task 是 Future 的子类，负责把协程包装起来并立即排入事件循环。
- asyncio.create_task() 会立刻开始调度，asyncio.ensure_future() 则兼容更多输入类型。

## 示例

```python
task = asyncio.create_task(fetch())
print(task.done())
await task
print(task.result())
```

## 易错点

- create_task 创建的 Task 必须被 await 或显式保存引用，否则可能被垃圾回收导致任务消失。

## 小结

Future 是结果容器，Task 是执行单元，日常开发几乎只用 Task。
