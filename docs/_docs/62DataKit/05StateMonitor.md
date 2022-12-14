---
title: StateMonitor
category: DataKit
order: 5
---

## StateMonitor
状态机, 主要负责处理交易时间

#### initialize
1. 传入"statemonitor.yaml"并解析配置`config`
2. 传入基础信息管理器`_bd_mgr`和数据管理器`_dt_mgr`
3. 遍历"statemonitor.yaml"中的"state"信息
- "inittime": 开盘时间
- "closetime": 收盘时间
- "proctime": 盘后处理时间
4. 根据"state"获取对应的"session.json"中的数据`ssInfo`
5. 将"state"填充至变量`sInfo`
6. 将`ssInfo`信息填充至`sInfo`(偏移后时间)
7. 将`sInfo`信息保存至`_map`
8. 遍历对应合约列表`pCommSet`判断当前是否是交易日

#### stop
停止状态机线程

#### run
启动状态机线程
1. 控制每隔1s执行一次
2. 遍历`_map`
3. 根据状态判断
**SS_ORIGINAL**
未初始化
1. 获取偏移后的时间
- offTime: 当前时间(分钟)
- offInitTime: 开盘时间
- offCloseTime: 收盘时间
- aucStartTime: 集合竞价时间
2. 遍历品种`pCommSet`
3. 判断是否是交易日
4. 根据当前时间跳转状态

**SS_INITIALIZED**
已初始化
1. 根据当前时间跳转状态

**SS_RECEIVING**
交易中
1. 如果当前已收盘, 跳转状态至`SS_CLOSED`
2. 如果当前盘中休息, 跳转状态`SS_PAUSED`

**SS_PAUSED**
休息中
1. 判断是否是节假日
2. 是节假日跳转状态``
3. 在盘中跳转状态`SS_RECEIVING`

**SS_CLOSED**
已收盘
1. 收盘作业时间跳转状态`SS_PROCING`
2. 盘后处理跳转状态`SS_PROCED`
3. 盘中休息跳转状态`SS_PAUSED`

**SS_PROCING**
收盘作业中, 直接跳转状态`SS_PROCED`

**SS_PROCED**
盘后已处理, 无操作

**SS_Holiday**
节假日
1.是节假日无操作, 否则跳转状态`SS_ORIGINAL`

#### 状态判断函数
- isAllInState: 是否所有品种处于某状态
- isAnyInState: 是否有品种处于某状态
- isInState: 某品种是否处于某状态
