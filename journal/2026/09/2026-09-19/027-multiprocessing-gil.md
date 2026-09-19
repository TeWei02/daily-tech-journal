# multiprocessing 与 GIL 的取舍：与相邻技术的配合

**日期**：2026-09-19　**领域**：Python　**编号**：27/115

## 背景

它很少单独出现，和上下游的约定决定了整体效果。这里围绕「multiprocessing 与 GIL 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- CPU 密集用多进程，IO 密集用线程或 asyncio
- 多进程传参需可 pickle，大对象建议用共享内存
- 跨组件问题先在边界处抓包或打日志。

## 示例

```python
with ProcessPoolExecutor(max_workers=8) as ex:
    results = list(ex.map(heavy, chunks))
```

## 易错点

- 子进程里的全局状态不会回传，注意初始化逻辑

## 小结

multiprocessing 与 GIL 的取舍 在与相邻技术的配合这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
