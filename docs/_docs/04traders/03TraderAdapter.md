---
title: TraderAdapter
category: traders
order: 3
---

## ParserAdapter
交易适配器, 继承了`ITraderSpi`, 很明显, 它的功能主要是处理交易回调

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
1. 将自己赋值给交易api的`m_sink`
2. 连接交易api

#### addSink
添加策略引擎, 保存在`_sinks`



#### addSink


#### getPosition


#### getOrders


#### getUndoneQty


#### enumPosition

#### openLong

#### openShort

#### closeLong



#### getOrders


#### closeShort


#### buy

#### sell

#### cancel

#### isTradeEnabled

#### checkCancelLimits


#### checkOrderLimits

#### checkSelfMatch

#### isSelfMatched

--- 


#### handleEvent

#### onLoginResult

#### onLogout

#### onRspEntrust

#### onRspAccount



#### onRspPosition



#### onRspOrders



#### onRspTrades


#### onPushOrder



#### onPushTrade


#### onTraderError



#### handleTraderLog



## TraderAdapterMgr
交易适配管理器, 主要负责同时管理多个交易适配器

#### run
启动所有交易适配器

#### addAdapter
添加交易适配器, 保存在`_adapters`