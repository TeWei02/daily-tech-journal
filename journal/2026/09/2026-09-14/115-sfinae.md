# 模板特化与 SFINAE：实现原理与内部机制

**日期**：2026-09-14　**领域**：C/C++　**编号**：115/115

## 背景

知道底层怎么走，行为异常时才能判断卡在哪一层。这里围绕「模板特化与 SFINAE」做一次整理，重点放在能直接落地的部分。

## 要点

- if constexpr 可替代大量 tag dispatch
- concept 让错误信息更友好
- 原理清楚后，参数上限与限制条件基本能自己推导。

## 示例

```cpp
template <class T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T> T twice(T v) { return v + v; }
```

## 易错点

- 特化必须在同一命名空间且在使用前声明

## 小结

模板特化与 SFINAE 在实现原理与内部机制这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
