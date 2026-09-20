# HTTP 缓存头优先级：代价与适用边界

**日期**：2026-09-20　**领域**：网络　**编号**：33/54

## 背景

任何方案都有不适用的时候，提前写清楚。这里围绕「HTTP 缓存头优先级」做一次整理，重点放在能直接落地的部分。

## 要点

- Cache-Control 的 max-age 覆盖 Expires，no-store 优先级最高
- ETag 与 Last-Modified 同时存在时 ETag 优先
- 把不适用条件写进文档，避免误用。

## 示例

```bash
Cache-Control: public, max-age=600, stale-while-revalidate=60
ETag: "v17"
```

## 易错点

- 命中协商缓存返回 304，仍要发一次请求

## 小结

HTTP 缓存头优先级 在代价与适用边界这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
