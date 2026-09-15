# aiohttp 会话复用与连接池

**日期**：2026-09-15　**领域**：Python　**系列**：Python 异步编程

## 一句话说明

避免为每次请求新建会话，理解连接池带来的收益。

## 关键点

- ClientSession 内部维护连接池，复用 TCP 连接可显著降低握手开销。
- 会话应尽量在应用生命周期内复用，并在退出时显式 close。
- 通过 TCPConnector(limit=...) 可以控制总连接数与单主机连接数。

## 代码 / 命令

```python
async with aiohttp.ClientSession() as session:
    async with session.get(url, timeout=10) as resp:
        data = await resp.json()
```

## 注意事项

- 每次请求都新建会话会导致连接无法复用，并发高时还会耗尽文件描述符。

## 小结

会话复用是异步 HTTP 性能的第一条优化。
