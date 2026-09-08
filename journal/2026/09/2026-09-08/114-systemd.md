# systemd 定时器的替代方案：实现原理与内部机制

**日期**：2026-09-08　**领域**：Linux　**编号**：114/115

## 背景

知道底层怎么走，行为异常时才能判断卡在哪一层。这里围绕「systemd 定时器的替代方案」做一次整理，重点放在能直接落地的部分。

## 要点

- OnCalendar 语法比 cron 更直观，且支持随机抖动
- 服务与定时器分离，用 systemctl list-timers 查看下次触发
- 原理清楚后，参数上限与限制条件基本能自己推导。

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

systemd 定时器的替代方案 在实现原理与内部机制这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
