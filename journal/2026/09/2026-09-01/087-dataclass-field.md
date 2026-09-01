# dataclass 的 field 与默认值：测试与验证策略

**日期**：2026-09-01　**领域**：Python　**编号**：87/115

## 背景

测试要覆盖正常、边界与失败三类路径。这里围绕「dataclass 的 field 与默认值」做一次整理，重点放在能直接落地的部分。

## 要点

- 可变默认值必须用 field(default_factory=list) 否则对象间共享同一列表
- frozen=True 可让实例可哈希，但嵌套可变字段仍可改
- 测试用例本身也要可维护。

## 示例

```python
@dataclass
class Job:
    name: str
    tags: list = field(default_factory=list)
    retries: int = 0
```

## 易错点

- 直接在类属性写 [] 会导致所有实例共享同一列表

## 小结

dataclass 的 field 与默认值 在测试与验证策略这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
