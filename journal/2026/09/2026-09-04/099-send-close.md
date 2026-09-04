# 生成器的 send 与 close：与相邻技术的配合

**日期**：2026-09-04　**领域**：Python　**编号**：99/115

## 背景

它很少单独出现，和上下游的约定决定了整体效果。这里围绕「生成器的 send 与 close」做一次整理，重点放在能直接落地的部分。

## 要点

- yield 表达式可接收 send 传入的值，首次必须先 next 或 send(None)
- GeneratorExit 用于清理，捕获后不要再 yield
- 跨组件问题先在边界处抓包或打日志。

## 示例

```python
def acc():
    total = 0
    while True:
        x = yield total
        if x is None:
            return
        total += x
```

## 易错点

- 在 finally 中 yield 会触发 RuntimeError

## 小结

生成器的 send 与 close 在与相邻技术的配合这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
