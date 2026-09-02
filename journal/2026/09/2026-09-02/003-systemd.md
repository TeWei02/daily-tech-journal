# systemd 定时器的替代方案：测试与验证策略

**日期**：2026-09-02　**领域**：Linux　**编号**：3/115

## 背景

测试要覆盖正常、边界与失败三类路径。这里围绕「systemd 定时器的替代方案」做一次整理，重点放在能直接落地的部分。

## 要点

- OnCalendar 语法比 cron 更直观，且支持随机抖动
- 服务与定时器分离，用 systemctl list-timers 查看下次触发
- 测试用例本身也要可维护。

## 示例

```bash
[Timer]
OnCalendar=*-*-* 03:00:00
Persistent=true

[Install]
WantedBy=timers.target
```

## 易错点

- 改了定时器要 daemon-reload 否则不生效

## 小结

systemd 定时器的替代方案 在测试与验证策略这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
