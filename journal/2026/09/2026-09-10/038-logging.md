# logging 的传播与层级：常见陷阱与错误示范

**日期**：2026-09-10　**领域**：Python　**编号**：38/99

## 背景

多数线上问题不是不会用，而是用错了一个细节。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 把踩过的坑写成检查项，比背结论更有效。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在常见陷阱与错误示范这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
