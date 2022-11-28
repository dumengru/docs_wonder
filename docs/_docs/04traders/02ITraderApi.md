---
title: ITraderApi
category: traders
order: 2
---

## 定义接口
打开"Product/WtCore/TraderAdapter.h"文件, 点击文件顶部`#include "../Includes/ITraderApi.h"`进入"ITraderApi.h"文件, 这里定义了行情解析模块接口

## ITraderSpi
交易回调接口

- handleTraderLog: 处理行情日志
- handleEvent: 处理交易接口事件
- onLoginResult: 登录回报
- onLogout: 注销回报
- onRspEntrust: 委托回报
- onRspAccount: 资金查询回报
- onRspPosition: 持仓查询回报
- onRspOrders：订单查询回报
- onRspTrades: 成交查询回报
- onRspSettlementInfo: 结算单查询回报
- onPushOrder: 订单回报推送
- onPushTrade: 成交回报推送
- onTraderError: 交易接口错误回报
- onPushInstrumentStatus: 合约状态推送

## ITraderApi
交易api管理接口

- init: 初始化接口(传入配置)
- release: 释放接口
- registerSpi: 注册回调接口
- connect: 连接交易服务器
- disconnect: 断开连接
- isConnected: 判断交易服务器是否连接
- makeEntrustID: 生成委托单号
- login: 登录接口
- logout: 注销接口
- orderInsert: 下单接口(下单的具体数据结构)
- orderAction: 订单操作接口(操作的具体数据结构)
- queryAccount: 查询账户信息
- queryPositions: 查询持仓信息
- queryOrders: 查询所有订单
- queryTrades: 查询成交明细
- querySettlement: 查询结算单

## 附加
- FuncCreateTrader: 获取`ITraderApi`的函数指针
- FuncDeleteTrader: 删除`ITraderApi`函数指针

