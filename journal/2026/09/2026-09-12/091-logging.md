# logging 的传播与层级：方案对比与选型

**日期**：2026-09-12　**领域**：Python　**编号**：91/115

## 背景

把候选方案的代价列清楚，选型就不再靠偏好。这里围绕「logging 的传播与层级」做一次整理，重点放在能直接落地的部分。

## 要点

- 子 logger 默认向父级传播，重复 handler 会导致日志翻倍
- 用 dictConfig 统一管理比手工 addHandler 清晰
- 选型结论要写清前提，否则换个环境就不成立。

## 示例

```python
log = logging.getLogger('app.db')
log.propagate = False
```

## 易错点

- 根 logger 上挂 handler 后再调用 basicConfig 无效

## 小结

logging 的传播与层级 在方案对比与选型这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
