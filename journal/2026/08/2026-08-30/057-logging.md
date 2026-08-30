# logging 的传播与层级：调试与观测手法

**日期**：2026-08-30　**领域**：Python　**编号**：57/115

## 背景

先拿到证据再改代码，日志与指标是第一手材料。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 把排查过程留成记录，下次能少走弯路。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在调试与观测手法这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
