# functools.lru_cache 的缓存键：性能与复杂度权衡

**日期**：2026-09-11　**领域**：Python　**编号**：24/115

## 背景

先量化再优化，凭感觉换实现经常得不偿失。这里围绕「functools.lru_cache 的缓存键」做一次整理，重点放在能直接落地的部分。

## 要点

- 参数必须可哈希，传 list 会直接 TypeError
- cache_info 的 hits/misses 是定位热点的第一手数据
- 优化前后都要有可复现的基准数据。

## 示例

```python
@lru_cache(maxsize=512)
def fetch(code: str, market: str) -> float:
    return _query(code, market)
```

## 易错点

- 带默认值的可选参数会造成多份缓存，建议显式传参

## 小结

functools.lru_cache 的缓存键 在性能与复杂度权衡这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
