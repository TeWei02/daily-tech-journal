# Kubernetes 探针设计：边界条件与异常路径

**日期**：2026-08-29　**领域**：工具　**编号**：71/115

## 背景

空集合、极值、超时、部分失败，这几类最容易漏。这里围绕「Kubernetes 探针设计」做一次整理，重点放在能直接落地的部分。

## 要点

- 存活探针用于重启恢复，就绪探针用于摘流量，语义不能混用
- 启动慢的服务用 startupProbe 避免被误杀
- 边界用例应固化成自动化测试。

## 示例

```yaml
startupProbe: { periodSeconds: 5, failureThreshold: 30 }
livenessProbe: { httpGet: { path: /healthz, port: 8080 } }
```

## 易错点

- 就绪探针依赖外部下游会导致整体抖动

## 小结

Kubernetes 探针设计 在边界条件与异常路径这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
