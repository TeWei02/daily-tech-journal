# multiprocessing 与 GIL 的取舍：性能与复杂度权衡

**日期**：2026-09-11　**领域**：Python　**编号**：26/115

## 背景

先量化再优化，凭感觉换实现经常得不偿失。这里围绕「multiprocessing 与 GIL 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- CPU 密集用多进程，IO 密集用线程或 asyncio
- 多进程传参需可 pickle，大对象建议用共享内存
- 优化前后都要有可复现的基准数据。

## 示例

```python
with ProcessPoolExecutor(max_workers=8) as ex:
    results = list(ex.map(heavy, chunks))
```

## 易错点

- 子进程里的全局状态不会回传，注意初始化逻辑

## 小结

multiprocessing 与 GIL 的取舍 在性能与复杂度权衡这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
