# CORS 预检请求触发条件：边界条件与异常路径

**日期**：2026-09-12　**领域**：Web　**编号**：51/115

## 背景

空集合、极值、超时、部分失败，这几类最容易漏。这里围绕「CORS 预检请求触发条件」做一次整理，重点放在能直接落地的部分。

## 要点

- 非简单方法或自定义头部会触发 OPTIONS 预检
- 带凭据时 Access-Control-Allow-Origin 不能为通配
- 边界用例应固化成自动化测试。

## 示例

```js
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

## 易错点

- 预检结果可缓存，但需要服务端给 Max-Age

## 小结

CORS 预检请求触发条件 在边界条件与异常路径这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
