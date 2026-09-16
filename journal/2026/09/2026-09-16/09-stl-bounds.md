# C++ 标准库中的 lower_bound 与 upper_bound

**日期**：2026-09-16　**领域**：算法与数据结构　**系列**：二分查找与边界处理 · 第 9 则

## 学习目标

熟悉标准库接口，避免重复造轮子。

## 核心要点

- 两者都在 <algorithm> 中，要求区间有序。
- 返回的是迭代器，做下标需要减去 begin()。
- 配合 lambda 比较器可以作用在自定义结构上。

## 示例

```python
auto it = std::lower_bound(v.begin(), v.end(), x);
int idx = int(it - v.begin());
bool found = (it != v.end() && *it == x);
```

## 易错点

- 在无序容器上调用会产生未定义行为，unordered_set 不适用。

## 小结

标准库版本经过充分优化，优先复用。
