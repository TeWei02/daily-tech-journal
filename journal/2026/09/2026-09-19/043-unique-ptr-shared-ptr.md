# unique_ptr 与 shared_ptr 的取舍：与相邻技术的配合

**日期**：2026-09-19　**领域**：C/C++　**编号**：43/115

## 背景

它很少单独出现，和上下游的约定决定了整体效果。这里围绕「unique_ptr 与 shared_ptr 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- 独占语义用 unique_ptr，零开销且可转 shared
- enable_shared_from_this 才能安全从成员函数返回自身
- 跨组件问题先在边界处抓包或打日志。

## 示例

```cpp
auto p = std::make_unique<Conn>(cfg);
std::shared_ptr<Conn> sp = std::move(p);
```

## 易错点

- shared_ptr 循环引用需要 weak_ptr 打破

## 小结

unique_ptr 与 shared_ptr 的取舍 在与相邻技术的配合这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
