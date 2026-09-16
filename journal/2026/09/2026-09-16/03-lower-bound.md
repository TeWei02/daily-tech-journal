# 寻找第一个不小于 target 的位置

**日期**：2026-09-16　**领域**：算法与数据结构　**系列**：二分查找与边界处理 · 第 3 则

## 学习目标

实现 lower_bound，作为后续二分变体的基础函数。

## 核心要点

- lower_bound 返回的是插入位置，即使 target 不存在也有意义。
- 判断条件写成 nums[mid] < target 时左移，等于时仍向右收缩可以拿到最后一个位置。
- 返回值范围在 0 到 n 之间，注意不是 n-1。

## 示例

```python
def lower_bound(nums, target):
    lo, hi = 0, len(nums)
    while lo < hi:
        mid = (lo + hi) // 2
        if nums[mid] < target:
            lo = mid + 1
        else:
            hi = mid
    return lo
```

## 易错点

- 返回下标可能等于数组长度，调用处直接取值会越界。

## 小结

lower_bound 把查找与插入位置统一起来。
