---
title: ParserCTP
category: parsers
order: 4
---

## ParserCTP
CTP系统行情接口, 继承了`IParserApi`, 很明显, 它的功能主要是管理行情api

同时继承了`CThostFtdcMdSpi`, 这是CTP系统提供的行情接口, CTP行情api管理必须继承该类

因此`ParserCTP`功能包括两部分, 一部分对接`IParserApi`, 实现行情登录, 连接, 订阅...等功能; 另一部分对接`CThostFtdcMdSpi`, 实现登录, 连接, 订阅, 行情...等响应

实际上`ParserCTP`既能管理行情api, 又能处理行情回调, 只不过它将行情回调的数据转移给了适配器进一步处理

---

> 对接`IParserApi`接口

#### init
通过配置初始化行情api

处理逻辑:
1. 获取登录配置(配置中有`localtime`专为测试使用)
2. 获取ctp行情dll文件名`ctpmodule`(这里命名与"ParserAdapter"冲突, 因此行情文件只能是"thostmduserapi_se")
3. 创建行情Api, 将自己注册为spi`m_pUserAPI->RegisterSpi(this)`, 注册前置地址(这里未执行初始化)

#### connect
初始化行情API`m_pUserAPI->Init()`

#### subscribe
1. 如果交易日正常则订阅合约列表
2. 通过行情api订阅市场行情`m_pUserAPI->SubscribeMarketData(subscribe, nCount)`
3. 通过行情适配器输出订阅日志

#### registerSpi
将行情适配器传递给`m_sink`, 行情适配器中的基础数据管理器传递给`m_pBaseDataMgr`

---

> 对接`CThostFtdcMdSpi`

#### OnFrontConnected
连接行情前置响应, 同时发起登录请求

#### OnRspUserLogin 
登录响应, 同时订阅行情数据(中间插入了一段对交易日判断的代码)

#### OnRtnDepthMarketData
订阅深度行情响应

处理逻辑
1. 如果没有基础数据管理直接返回
2. 如果基础数据管理器找不到合约, 直接返回
3. 处理交易日时间
4. 获取合约信息, 填充tick数据
5. 将数据回传给行情适配器处理

#### OnRspSubMarketData
订阅市场行情响应, 无操作

#### OnHeartBeatWarning
心跳通知, 通过行情适配器发送心跳日志

#### OnRspUserLogout 
登出响应

#### OnFrontDisconnected
断开行情前置连接响应

#### OnRspUnSubMarketData
取消订阅响应, 无操作
