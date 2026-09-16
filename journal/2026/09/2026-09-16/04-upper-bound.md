# 寻找最后一个不大于 target 的位置

**日期**：2026-09-16　**领域**：算法与数据结构　**系列**：二分查找与边界处理

## 一句话说明

与 lower_bound 对照记忆 upper_bound 的差异。

## 关键点

- upper_bound 找到的是第一个大于 target 的位置，减一即最后一个不大于 target 的位置。
- 把判断条件从 < 换成 <= 就能在两种语义间切换。
- 配合 lower_bound 可以数出某个值在有序数组中的出现次数。

## 代码 / 命令

```python
def upper_bound(nums, target):
    lo, hi = 0, len(nums)
    while lo < hi:
        mid = (lo + hi) // 2
        if nums[mid] <= target:
            lo = mid + 1
        else:
            hi = mid
    return lo

count = upper_bound(nums, t) - lower_bound(nums, t)
```

## 注意事项

- 把 upper_bound 的结果直接当作下标使用会偏移一位。

## 小结

二分查找的两把标尺：lower_bound 与 upper_bound。
