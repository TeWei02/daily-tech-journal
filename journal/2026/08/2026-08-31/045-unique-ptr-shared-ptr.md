# unique_ptr 与 shared_ptr 的取舍：版本迁移与兼容处理

**日期**：2026-08-31　**领域**：C/C++　**编号**：45/115

## 背景

升级前先确认依赖链上的行为差异。这里围绕「unique_ptr 与 shared_ptr 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- 独占语义用 unique_ptr，零开销且可转 shared
- enable_shared_from_this 才能安全从成员函数返回自身
- 灰度期间保留回退路径。

## 示例

```cpp
auto p = std::make_unique<Conn>(cfg);
std::shared_ptr<Conn> sp = std::move(p);
```

## 易错点

- shared_ptr 循环引用需要 weak_ptr 打破

## 小结

unique_ptr 与 shared_ptr 的取舍 在版本迁移与兼容处理这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
