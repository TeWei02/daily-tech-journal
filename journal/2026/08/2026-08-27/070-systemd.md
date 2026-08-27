# systemd 定时器的替代方案：常见陷阱与错误示范

**日期**：2026-08-27　**领域**：Linux　**编号**：70/115

## 背景

多数线上问题不是不会用，而是用错了一个细节。这里围绕「systemd 定时器的替代方案」做一次整理，重点放在能直接落地的部分。

## 要点

- OnCalendar 语法比 cron 更直观，且支持随机抖动
- 服务与定时器分离，用 systemctl list-timers 查看下次触发
- 把踩过的坑写成检查项，比背结论更有效。

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

systemd 定时器的替代方案 在常见陷阱与错误示范这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
