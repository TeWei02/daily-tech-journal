# logging 的传播与层级：线上问题复盘

**日期**：2026-09-03　**领域**：Python　**编号**：42/115

## 背景

复盘只谈事实与改进项，不追责个人。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 每个改进项都要有负责人与截止时间。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在线上问题复盘这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
