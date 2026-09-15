# 常见性能陷阱与排查思路

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程

## 一句话说明

识别会拖垮事件循环的写法。

## 关键点

- time.sleep、requests、同步文件 IO 都会阻塞整个事件循环。
- 排查时可以在慢操作前后打印时间差，或使用 asyncio 的调试模式。
- 启用 PYTHONASYNCIODEBUG=1 或 loop.set_debug(True) 能提示执行过久的回调。

## 代码 / 命令

```python
loop = asyncio.get_running_loop()
loop.set_debug(True)
loop.slow_callback_duration = 0.05
```

## 注意事项

- 只在测试环境观察不到阻塞问题，压测时才会集中暴露。

## 小结

异步代码第一守则是绝不阻塞事件循环。
