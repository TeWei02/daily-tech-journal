# 管道与重定向的语义

**日期**：2026-09-17　**领域**：Linux 与工程实践　**系列**：Linux 命令行与 Shell · 第 5 则

## 学习目标

分清标准输入输出的流向与常见组合。

## 核心要点

- | 把前一命令的 stdout 作为后一命令的 stdin。
- 2> 重定向 stderr，&> 同时重定向 stdout 和 stderr。
- tee 可以一边写文件一边输出到屏幕，便于保留日志。

## 示例

```bash
make 2>&1 | tee build.log
grep error app.log > errors.txt 2>&1
```

## 易错点

- 只重定向 stdout 会漏掉错误信息，排查时容易误判。

## 小结

理解流的走向，组合命令才不会出错。
