# functools.lru_cache 的缓存键：方案对比与选型

**日期**：2026-08-29　**领域**：Python　**编号**：79/115

## 背景

把候选方案的代价列清楚，选型就不再靠偏好。这里围绕「functools.lru_cache 的缓存键」做一次整理，重点放在能直接落地的部分。

## 要点

- 参数必须可哈希，传 list 会直接 TypeError
- cache_info 的 hits/misses 是定位热点的第一手数据
- 选型结论要写清前提，否则换个环境就不成立。

## 示例

```python
@lru_cache(maxsize=512)
def fetch(code: str, market: str) -> float:
    return _query(code, market)
```

## 易错点

- 带默认值的可选参数会造成多份缓存，建议显式传参

## 小结

functools.lru_cache 的缓存键 在方案对比与选型这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
