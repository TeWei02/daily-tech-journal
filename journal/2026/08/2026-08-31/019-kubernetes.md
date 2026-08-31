# Kubernetes 探针设计：调试与观测手法

**日期**：2026-08-31　**领域**：工具　**编号**：19/115

## 背景

先拿到证据再改代码，日志与指标是第一手材料。这里围绕「Kubernetes 探针设计」做一次整理，重点放在能直接落地的部分。

## 要点

- 存活探针用于重启恢复，就绪探针用于摘流量，语义不能混用
- 启动慢的服务用 startupProbe 避免被误杀
- 把排查过程留成记录，下次能少走弯路。

## 示例

```yaml
startupProbe: { periodSeconds: 5, failureThreshold: 30 }
livenessProbe: { httpGet: { path: /healthz, port: 8080 } }
```

## 易错点

- 就绪探针依赖外部下游会导致整体抖动

## 小结

Kubernetes 探针设计 在调试与观测手法这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
