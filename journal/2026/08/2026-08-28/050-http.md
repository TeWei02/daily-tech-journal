# HTTP 缓存头优先级：性能与复杂度权衡

**日期**：2026-08-28　**领域**：网络　**编号**：50/115

## 背景

先量化再优化，凭感觉换实现经常得不偿失。这里围绕「HTTP 缓存头优先级」做一次整理，重点放在能直接落地的部分。

## 要点

- Cache-Control 的 max-age 覆盖 Expires，no-store 优先级最高
- ETag 与 Last-Modified 同时存在时 ETag 优先
- 优化前后都要有可复现的基准数据。

## 示例

```bash
Cache-Control: public, max-age=600, stale-while-revalidate=60
ETag: "v17"
```

## 易错点

- 命中协商缓存返回 304，仍要发一次请求

## 小结

HTTP 缓存头优先级 在性能与复杂度权衡这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
