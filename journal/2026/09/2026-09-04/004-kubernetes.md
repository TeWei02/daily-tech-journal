# Kubernetes 探针设计：线上问题复盘

**日期**：2026-09-04　**领域**：工具　**编号**：4/115

## 背景

复盘只谈事实与改进项，不追责个人。这里围绕「Kubernetes 探针设计」做一次整理，重点放在能直接落地的部分。

## 要点

- 存活探针用于重启恢复，就绪探针用于摘流量，语义不能混用
- 启动慢的服务用 startupProbe 避免被误杀
- 每个改进项都要有负责人与截止时间。

## 示例

```yaml
startupProbe: { periodSeconds: 5, failureThreshold: 30 }
livenessProbe: { httpGet: { path: /healthz, port: 8080 } }
```

## 易错点

- 就绪探针依赖外部下游会导致整体抖动

## 小结

Kubernetes 探针设计 在线上问题复盘这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
