# functools.lru_cache 的缓存键：代码评审关注点

**日期**：2026-09-23　**领域**：Python　**编号**：19/104

## 背景

评审优先看契约与失败路径，其次才是实现技巧。这里围绕「functools.lru_cache 的缓存键」做一次整理，重点放在能直接落地的部分。

## 要点

- 参数必须可哈希，传 list 会直接 TypeError
- cache_info 的 hits/misses 是定位热点的第一手数据
- 把重复出现的意见沉淀成团队约定。

## 示例

```python
@lru_cache(maxsize=512)
def fetch(code: str, market: str) -> float:
    return _query(code, market)
```

## 易错点

- 带默认值的可选参数会造成多份缓存，建议显式传参

## 小结

functools.lru_cache 的缓存键 在代码评审关注点这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
