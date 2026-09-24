# logging 的传播与层级：实现原理与内部机制

**日期**：2026-09-24　**领域**：Python　**编号**：97/104

## 背景

知道底层怎么走，行为异常时才能判断卡在哪一层。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 原理清楚后，参数上限与限制条件基本能自己推导。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在实现原理与内部机制这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
