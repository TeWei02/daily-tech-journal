# 模板特化与 SFINAE：性能与复杂度权衡

**日期**：2026-09-11　**领域**：C/C++　**编号**：45/115

## 背景

先量化再优化，凭感觉换实现经常得不偿失。这里围绕「模板特化与 SFINAE」做一次整理，重点放在能直接落地的部分。

## 要点

- if constexpr 可替代大量 tag dispatch
- concept 让错误信息更友好
- 优化前后都要有可复现的基准数据。

## 示例

```cpp
template <class T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T> T twice(T v) { return v + v; }
```

## 易错点

- 特化必须在同一命名空间且在使用前声明

## 小结

模板特化与 SFINAE 在性能与复杂度权衡这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
