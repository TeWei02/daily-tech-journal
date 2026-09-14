# logging 的传播与层级：基础用法与最小示例

**日期**：2026-09-14　**领域**：Python　**编号**：9/115

## 背景

先写出能跑通的最小示例，把输入输出钉死，再谈扩展。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 最小示例留着，回归时可直接复用。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在基础用法与最小示例这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
