# HTTP 缓存头优先级：重构与可维护性

**日期**：2026-09-17　**领域**：网络　**编号**：22/115

## 背景

先把行为固定住再改结构，避免同时改两件事。这里围绕「HTTP 缓存头优先级」做一次整理，重点放在能直接落地的部分。

## 要点

- Cache-Control 的 max-age 覆盖 Expires，no-store 优先级最高
- ETag 与 Last-Modified 同时存在时 ETag 优先
- 重构后接口不变，调用方无感。

## 示例

```bash
Cache-Control: public, max-age=600, stale-while-revalidate=60
ETag: "v17"
```

## 易错点

- 命中协商缓存返回 304，仍要发一次请求

## 小结

HTTP 缓存头优先级 在重构与可维护性这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
