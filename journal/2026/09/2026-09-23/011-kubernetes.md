# Kubernetes 探针设计：小规模验证方法

**日期**：2026-09-23　**领域**：工具　**编号**：11/104

## 背景

先用小样本验证假设，再决定是否推广。这里围绕「Kubernetes 探针设计」做一次整理，重点放在能直接落地的部分。

## 要点

- 存活探针用于重启恢复，就绪探针用于摘流量，语义不能混用
- 启动慢的服务用 startupProbe 避免被误杀
- 试点结论要能复现。

## 示例

```yaml
startupProbe: { periodSeconds: 5, failureThreshold: 30 }
livenessProbe: { httpGet: { path: /healthz, port: 8080 } }
```

## 易错点

- 就绪探针依赖外部下游会导致整体抖动

## 小结

Kubernetes 探针设计 在小规模验证方法这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
