# 文件查找：find 的常用表达式

**日期**：2026-09-17　**领域**：Linux 与工程实践　**系列**：Linux 命令行与 Shell · 第 1 则

## 学习目标

熟练使用 find 按名称、时间、大小定位文件。

## 核心要点

- -name 支持通配符，-iname 忽略大小写。
- -mtime -7 表示最近 7 天修改过的文件，-mmin 以分钟为单位。
- -exec 与 xargs 可以接后续处理，注意 xargs 的 -0 配合 -print0 处理含空格文件名。

## 示例

```bash
find /var/log -type f -name '*.log' -mtime -7 -size +10M
find . -name '*.tmp' -print0 | xargs -0 rm -f
```

## 易错点

- 忘记 -type f 会把目录也匹配进来；删除操作务必先空跑确认。

## 小结

find 是文件定位的瑞士军刀。
