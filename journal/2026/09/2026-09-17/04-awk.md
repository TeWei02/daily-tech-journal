# 字段处理：awk 的统计能力

**日期**：2026-09-17　**领域**：Linux 与工程实践　**系列**：Linux 命令行与 Shell

## 一句话说明

用 awk 做列提取与简单聚合。

## 关键点

- $1、$2 表示第几列，NF 是字段数，NR 是行号。
- -F 指定分隔符，处理 CSV 与日志时非常有用。
- END 块里做汇总，可替代简单的 sort | uniq -c 统计。

## 代码 / 命令

```bash
awk -F, '{sum += $3} END {print sum}' data.csv
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head
```

## 注意事项

- 默认按空白分隔，字段内含空格时需要显式指定 -F。

## 小结

awk 是命令行里的轻量数据处理语言。
