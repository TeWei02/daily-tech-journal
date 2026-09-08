# unique_ptr 与 shared_ptr 的取舍：基础用法与最小示例

**日期**：2026-09-08　**领域**：C/C++　**编号**：15/115

## 背景

先写出能跑通的最小示例，把输入输出钉死，再谈扩展。这里围绕「unique_ptr 与 shared_ptr 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- 独占语义用 unique_ptr，零开销且可转 shared
- enable_shared_from_this 才能安全从成员函数返回自身
- 最小示例留着，回归时可直接复用。

## 示例

```cpp
auto p = std::make_unique<Conn>(cfg);
std::shared_ptr<Conn> sp = std::move(p);
```

## 易错点

- shared_ptr 循环引用需要 weak_ptr 打破

## 小结

unique_ptr 与 shared_ptr 的取舍 在基础用法与最小示例这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
