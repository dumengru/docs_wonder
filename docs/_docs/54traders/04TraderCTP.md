---
title: TraderCTP
category: Traders
order: 4
---

## TraderCTP
`ParserCTP`功能包括两部分, 一部分对接`IParserApi`, 实现行情登录, 连接, 订阅...等功能; 另一部分对接`CThostFtdcMdSpi`, 实现登录, 连接, 订阅, 行情...等响应

---

> 对接`IParserApi`接口

#### init
初始化
1. 获取交易相关配置
2. 获取交易api构建函数`m_funcCreator`

#### registerSpi
将适配器传递给`m_sink`

#### makeEntrustID
创建报单id

#### connect
连接交易api
1. 创建交易api`m_pUserAPI`
2. 将自己注册为spi
3. 注册公有流和私有流
4. 注册交易前置
5. 初始化交易api
6. 创建一个线程循环, 专门执行队列`m_queQuery`中的查询函数

#### disconnect
断开交易api连接

#### login
交易api登录认证

#### logout
交易api退出登录

#### orderInsert
发送订单
1. 创建报单结构体`req`
2. 填充报单结构体
3. 通过交易api发送报单

#### orderAction
发送撤单/改单
1. 创建报单操作结构体`req`
2. 填充报单操作结构体
3. 通过交易api发送报单操作

#### queryAccount/queryPositions/queryOrders/queryTrades/querySettlement
查询数据
1. 填充查询请求结构体
2. 向队列`m_queQuery`中添加利用交易api发送的查询请求

---

> 对接`CThostFtdcTraderSpi`接口

#### OnFrontConnected
交易前置服务器连接回调
1. 通过交易适配器处理连接事件

#### OnHeartBeatWarning
通过交易适配器发送心跳日志

#### OnRspAuthenticate
交易api认证响应

#### OnRspUserLogin
交易api登录响应

#### OnRspSettlementInfoConfirm
结算结果确认响应

#### OnRspQrySettlementInfoConfirm
查询结算信息确认响应

#### OnRspQryTradingAccount
查询资金账户响应
1. 更新账户资金信息`accountInfo`
2. 回调适配器处理查询结果`m_sink->onRspAccount`

#### OnRspOrderInsert
报单录入请求响应
1. 获取输入报单`entrust`
2. 回调适配器处理`m_sink->onRspEntrust`

#### OnRspOrderAction
(...未完待续)

#### OnRspQryInvestorPosition
查询投资者持仓响应
1. 获取合约, 品种信息
2. 更新持仓数据`pos`, 保存在`m_mapPosition`
3. 回调适配器处理`m_sink->onRspPosition`

#### OnRspQryTrade
查询成交响应
1. 回调适配器处理`m_sink->onRspTrades`

#### OnRspQryOrder
查询报单响应
1. 回调适配器处理`m_sink->onRspOrders`

#### OnRspError
无操作

#### OnRtnOrder
报单通知
1. 获取订单信息
2. 回调适配器处理`m_sink->onPushOrder`

#### OnRtnTrade
成交通知
1. 获取成交信息
2. 回调适配器处理`m_sink->onPushTrade`

#### OnErrRtnOrderInsert
报单录入错误回报
1. 获取输入订单
2. 回调适配器处理`m_sink->onRspEntrus`

#### OnRtnInstrumentStatus
合约交易状态通知
1. 回调适配器处理`m_sink->onPushInstrumentStatus`
