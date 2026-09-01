# HTTP 缓存头优先级：并发与线程安全

**日期**：2026-09-01　**领域**：网络　**编号**：35/115

## 背景

共享可变状态是并发问题的根源，能消除就消除。这里围绕「HTTP 缓存头优先级」做一次整理，重点放在能直接落地的部分。

## 要点

- Cache-Control 的 max-age 覆盖 Expires，no-store 优先级最高
- ETag 与 Last-Modified 同时存在时 ETag 优先
- 并发缺陷难以复现，需靠压测与竞态注入暴露。

## 示例

```bash
Cache-Control: public, max-age=600, stale-while-revalidate=60
ETag: "v17"
```

## 易错点

- 命中协商缓存返回 304，仍要发一次请求

## 小结

HTTP 缓存头优先级 在并发与线程安全这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
