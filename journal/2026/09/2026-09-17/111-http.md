# HTTP 缓存头优先级：线上问题复盘

**日期**：2026-09-17　**领域**：网络　**编号**：111/115

## 背景

复盘只谈事实与改进项，不追责个人。这里围绕「HTTP 缓存头优先级」做一次整理，重点放在能直接落地的部分。

## 要点

- Cache-Control 的 max-age 覆盖 Expires，no-store 优先级最高
- ETag 与 Last-Modified 同时存在时 ETag 优先
- 每个改进项都要有负责人与截止时间。

## 示例

```bash
Cache-Control: public, max-age=600, stale-while-revalidate=60
ETag: "v17"
```

## 易错点

- 命中协商缓存返回 304，仍要发一次请求

## 小结

HTTP 缓存头优先级 在线上问题复盘这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
