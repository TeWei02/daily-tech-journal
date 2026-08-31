# 模板特化与 SFINAE：版本迁移与兼容处理

**日期**：2026-08-31　**领域**：C/C++　**编号**：48/115

## 背景

升级前先确认依赖链上的行为差异。这里围绕「模板特化与 SFINAE」做一次整理，重点放在能直接落地的部分。

## 要点

- if constexpr 可替代大量 tag dispatch
- concept 让错误信息更友好
- 灰度期间保留回退路径。

## 示例

```cpp
template <class T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T> T twice(T v) { return v + v; }
```

## 易错点

- 特化必须在同一命名空间且在使用前声明

## 小结

模板特化与 SFINAE 在版本迁移与兼容处理这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
