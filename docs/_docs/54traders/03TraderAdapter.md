---
title: TraderAdapter
category: traders
order: 3
---

## ParserAdapter
交易适配器, 继承了`ITraderSpi`, 很明显, 它的功能主要是处理交易回调. 这里适配器同时包含了交易相关功能

#### 枚举
- tagAdapterState: 适配器状态
- _PosItem: 持仓数据
- _RiskParams: 订单数据

#### init
默认初始化(需要配置), 传入参数
_id: 交易适配器id
- _policy_mgr: 交易规则管理器
- _bd_mgr: 基础数据管理器
- _trader_api: 交易api
- _save_data: 是否保存交易数据

1. 解析流量风控参数
2. 创建交易api`_trader_api`
3. 通过参数初始化交易api

#### initExt
初始化执行器(不需要配置), 传入参数
_id: 交易适配器id
- _policy_mgr: 交易规则管理器
- _bd_mgr: 基础数据管理器
- _trader_api: 交易api
- _save_data: 是否保存交易数据

1. 获取交易api
2. 初始化交易api

#### run
1. 将自己传递给交易api的`m_sink`
2. 连接交易api

#### addSink
添加策略引擎, 保存在`_sinks`

---

**交易功能**

#### getPosition
1. flag==1: 统计多头持仓
2. flag==2: 统计空头持仓
3. flag==3: 统计净持仓

#### getOrders
若stdCode == "", 获取全部订单; 否则获取指定品种订单

#### getUndoneQty
获取未完成订单数量

#### enumPosition
通过输入回调函数枚举持仓信息

#### openLong/openShort/closeLong/closeShort
1. 创建订单结构
2. 设置下单合约
3. 如果price==0.0是市价单; 否则限价单
4. 设置订单标志
- flag==0, 普通订单
- flag==1, fak
- flag==2, fok
5. 设置多空方向
6. 设置开平方向
7. 发出订单

#### buy/sell
1. 判断下单量
2. 判断是否自成交
3. 获取合约信息, 品种信息, 交易时间
4. 更新未完成订单量
5. 获取持仓信息
6. 获取统计数据
7. 获取品种交易规则组
8. 获取最大下单量`unitQty`
9. 遍历交易规则
- 如果设置了开仓规则
    1. 检查开仓限制
    2. 检查单笔最大委托量
- 如果设置了平今规则
    1. 检查可平今仓
    2. 检查单笔最大委托量
- 如果设置了平昨规则: ...
- 如果只设置了平仓规则: ...

#### cancel
1. 通过订单id或指定条件撤单

#### isTradeEnabled
1. 判断是否开启风控
2. 如果品种被禁止交易, 则返回false

#### checkCancelLimits/checkOrderLimits
检查撤单限制
1. 判断是否开启风控
2. 判断品种是否被禁止交易
3. 获取风控参数
4. 获取品种交易信息
5. 判断撤单次数是否超过风控限制
6. 检查撤单频率

#### checkSelfMatch
检查自成交

#### isSelfMatched
判断是否自成交

---

**回调功能**

#### handleEvent
处理交易事件

#### onLoginResult
登录回调

#### onLogout
登出回调, 无操作

#### onRspEntrust
下单报错回调
1. 输出报错信息
2. 获取合约和品种信息
3. 获取品种标准代码
4. 输出详细信息
5. 如果未完成订单==0, 直接返回, 否则更新未完成订单
6. 回调策略`sink->on_entrust`
7. 输出通知信息

#### onRspAccount
账户变动回调
1. 保存账户数据
2. 回调策略`sink->on_account`
3. 更新交易状态, 回调策略`sink->on_channel_ready`

#### onRspPosition
持仓变动回调
1. 遍历持仓信息`pItem`
2. 获取合约, 品种信息, 合约标准码
3. 获取持仓数据`pos`
4. 根据持仓信息更新持仓数据
5. 遍历持仓数据, 回调策略`sink->on_position`

#### onRspOrders
订单变动回调
1. 清空未完成订单量
2. 遍历订单信息`orderInfo`
3. 获取合约, 品种信息, 合约标准码
4. 更新交易统计数据`statItem`
5. 更新未完成订单量`_undone_qty`
6. 回调交易api, 查询成交明细`_trader_api->queryTrades`

#### onRspTrades
成交变动回调
1. 遍历成交信息`tInfo`
2. 获取合约, 品种信息, 合约标准码
3. 更新交易统计数据`statItem`
4. 回调交易api, 查询账户信息`_trader_api->queryAccount`

#### onPushOrder
订单推送回调

(...未完待续)

#### onPushTrade
成交推送回调

(...未完待续)

#### onTraderError
1. 如果有报错, 输出日志
2. 通过UDP广播通知交易报错信息

#### handleTraderLog
输出交易日志


## TraderAdapterMgr
交易适配管理器, 主要负责同时管理多个交易适配器

#### run
启动所有交易适配器

#### addAdapter
添加交易适配器, 保存在`_adapters`