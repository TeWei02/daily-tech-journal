# CORS 预检请求触发条件：版本迁移与兼容处理

**日期**：2026-08-31　**领域**：Web　**编号**：80/115

## 背景

升级前先确认依赖链上的行为差异。这里围绕「CORS 预检请求触发条件」做一次整理，重点放在能直接落地的部分。

## 要点

- 非简单方法或自定义头部会触发 OPTIONS 预检
- 带凭据时 Access-Control-Allow-Origin 不能为通配
- 灰度期间保留回退路径。

## 示例

```js
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

## 易错点

- 预检结果可缓存，但需要服务端给 Max-Age

## 小结

CORS 预检请求触发条件 在版本迁移与兼容处理这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
