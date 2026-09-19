# 模板特化与 SFINAE：与相邻技术的配合

**日期**：2026-09-19　**领域**：C/C++　**编号**：46/115

## 背景

它很少单独出现，和上下游的约定决定了整体效果。这里围绕「模板特化与 SFINAE」做一次整理，重点放在能直接落地的部分。

## 要点

- if constexpr 可替代大量 tag dispatch
- concept 让错误信息更友好
- 跨组件问题先在边界处抓包或打日志。

## 示例

```cpp
template <class T>
concept Numeric = std::is_arithmetic_v<T>;

template <Numeric T> T twice(T v) { return v + v; }
```

## 易错点

- 特化必须在同一命名空间且在使用前声明

## 小结

模板特化与 SFINAE 在与相邻技术的配合这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
