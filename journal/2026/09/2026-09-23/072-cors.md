# CORS 预检请求触发条件：代码评审关注点

**日期**：2026-09-23　**领域**：Web　**编号**：72/104

## 背景

评审优先看契约与失败路径，其次才是实现技巧。这里围绕「CORS 预检请求触发条件」做一次整理，重点放在能直接落地的部分。

## 要点

- 非简单方法或自定义头部会触发 OPTIONS 预检
- 带凭据时 Access-Control-Allow-Origin 不能为通配
- 把重复出现的意见沉淀成团队约定。

## 示例

```js
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

## 易错点

- 预检结果可缓存，但需要服务端给 Max-Age

## 小结

CORS 预检请求触发条件 在代码评审关注点这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
