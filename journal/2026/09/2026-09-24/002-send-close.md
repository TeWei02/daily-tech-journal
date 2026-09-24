# 生成器的 send 与 close：基础用法与最小示例

**日期**：2026-09-24　**领域**：Python　**编号**：2/104

## 背景

先写出能跑通的最小示例，把输入输出钉死，再谈扩展。这里围绕「生成器的 send 与 close」做一次整理，重点放在能直接落地的部分。

## 要点

- yield 表达式可接收 send 传入的值，首次必须先 next 或 send(None)
- GeneratorExit 用于清理，捕获后不要再 yield
- 最小示例留着，回归时可直接复用。

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

生成器的 send 与 close 在基础用法与最小示例这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
