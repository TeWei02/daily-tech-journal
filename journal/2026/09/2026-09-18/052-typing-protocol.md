# typing.Protocol 做结构化子类型：配置与参数调优

**日期**：2026-09-18　**领域**：Python　**编号**：52/115

## 背景

参数调整必须一次只改一个，否则无法归因。这里围绕「typing.Protocol 做结构化子类型」做一次整理，重点放在能直接落地的部分。

## 要点

- 不需要继承即可满足协议，适合给第三方库对象做适配层
- runtime_checkable 只检查方法是否存在，不检查签名
- 调优结论要绑定当时的负载特征。

## 示例

```python
class Reader(Protocol):
    def read(self, n: int) -> bytes: ...

def consume(r: Reader) -> bytes:
    return r.read(1024)
```

## 易错点

- 误把 Protocol 当基类实例化会报错

## 小结

typing.Protocol 做结构化子类型 在配置与参数调优这一面，结论可以归纳为：把前提写清楚、把失败路径覆盖到，剩下的就是按数据调优。
