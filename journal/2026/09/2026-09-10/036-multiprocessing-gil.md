# multiprocessing 与 GIL 的取舍：常见陷阱与错误示范

**日期**：2026-09-10　**领域**：Python　**编号**：36/99

## 背景

多数线上问题不是不会用，而是用错了一个细节。这里围绕「multiprocessing 与 GIL 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- CPU 密集用多进程，IO 密集用线程或 asyncio
- 多进程传参需可 pickle，大对象建议用共享内存
- 把踩过的坑写成检查项，比背结论更有效。

## 示例

```python
with ProcessPoolExecutor(max_workers=8) as ex:
    results = list(ex.map(heavy, chunks))
```

## 易错点

- 子进程里的全局状态不会回传，注意初始化逻辑

## 小结

multiprocessing 与 GIL 的取舍 在常见陷阱与错误示范这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
