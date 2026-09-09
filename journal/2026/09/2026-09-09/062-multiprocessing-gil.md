# multiprocessing 与 GIL 的取舍：落到真实场景的改造

**日期**：2026-09-09　**领域**：Python　**编号**：62/115

## 背景

把它放进真实流程，通常要补上配置、日志与失败分支。这里围绕「multiprocessing 与 GIL 的取舍」做一次整理，重点放在能直接落地的部分。

## 要点

- CPU 密集用多进程，IO 密集用线程或 asyncio
- 多进程传参需可 pickle，大对象建议用共享内存
- 改造后别忘了补一次端到端验证。

## 示例

```python
with ProcessPoolExecutor(max_workers=8) as ex:
    results = list(ex.map(heavy, chunks))
```

## 易错点

- 子进程里的全局状态不会回传，注意初始化逻辑

## 小结

multiprocessing 与 GIL 的取舍 在落到真实场景的改造这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
