---
title: WtDataWriter
category: DataKit
order: 4
---

## WtDataWriter
继承`IDataWriter`

#### init
1. 传入配置"dtcfg.yaml"中的"writer"
- "savelog": 是否保存日志
- "path": 数据存储路径
- "cache": 缓存文件名称
- "async": 是否异步写入数据
- "groupsize": 每隔多少天数据输出一条日志
- "disablehis": 是否禁用历史数据
- "disable...": 不保存...数据
2. 加载tick缓存`loadCache`

#### 写入数据方法(略)
- writeTick: 写入tick数据(略)
- writeOrderQueue
- writeOrderDetail
- writeTransaction

#### transHisData
收盘作业(略)
