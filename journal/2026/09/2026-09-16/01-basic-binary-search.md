# 二分查找的基本形式

**日期**：2026-09-16　**领域**：算法与数据结构　**系列**：二分查找与边界处理 · 第 1 则

## 学习目标

先把最朴素的写法写对，再讨论边界变体。

## 核心要点

- 二分查找要求序列有序，通过不断折半把查找区间缩小一半。
- 循环不变量是解题关键：每一轮都要明确答案落在哪个区间内。
- 时间复杂度 O(log n)，远优于顺序扫描的 O(n)。

## 示例

```python
def search(nums, target):
    lo, hi = 0, len(nums) - 1
    while lo <= hi:
        mid = (lo + hi) // 2
        if nums[mid] == target:
            return mid
        if nums[mid] < target:
            lo = mid + 1
        else:
            hi = mid - 1
    return -1
```

## 易错点

- mid 用 (lo+hi)//2 在超大数组下标下可能溢出，Java 场景需写成 lo + (hi-lo)/2。

## 小结

写对循环不变量，二分就不会错。
