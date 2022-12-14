---
title: IParserApi
category: Parsers
order: 2
---

## 定义接口
打开"Product/WtCore/ParserAdapter.h"文件(注意该文件和"DataKit/WtDtCore/ParserAdapter.h"不一样), 点击文件顶部`#include "../Includes/IParserApi.h`进入"IParderApi.h"文件, 这里定义了行情解析模块接口

## IParserSpi
行情回调接口

- handleEvent: 处理事件
- handleSymbolList: 处理合约列表
- handleQuote: 处理实时行情
- handleOrderQueue: 处理订单委托队列
- handleOrderDetail: 处理逐笔委托数据
- handleTransaction: 处理逐笔成交数据
- handleParserLog: 处理行情日志

## IParserApi
行情api管理接口

- init: 初始化接口(传入配置)
- release: 释放接口
- connect: 连接行情服务器
- disconnect: 断开行情服务器连接
- isConnected: 判断行情服务器是否连接
- subscribe: 订阅合约(传入合约列表)
- unsubscribe: 取消订阅(传入合约列表)
- registerSpi: 注册回调接口

## 附加
- FuncCreateParser: 获取`IParserApi`的函数指针
- FuncDeleteParser: 删除`IParserApi`函数指针
