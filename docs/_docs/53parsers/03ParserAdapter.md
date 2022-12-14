---
title: ParserAdapter
category: Parsers
order: 3
---

## IParserStub
这是数据落地接口类, 比如交易引擎会继承该类, 并实现相关方法

1. handle_push_quote: 处理实时行情推送
2. handle_push_order_detail: 处理逐笔委托数据推送
3. handle_push_order_queue: 处理订单委托队列推送
4. handle_push_transaction: 处理逐笔成交数据推送

## ParserAdapter
行情适配器, 继承了`IParserSpi`, 很明显, 它的功能主要是处理行情回调.(boost::noncopyable, 限制该类为单例类)

#### ParserAdapter
构造函数传入
- `_bd_mgr`: 基础信息管理器`WTSBaseDataMgr`
- `_dt_mgr`: 数据管理器`DataManager`
- `_idx_fact`: 指数工厂

#### init
默认初始化(需要配置), 传入参数
- _id: 适配器id
- _cfg: 适配器配置
- _stub: 数据落地对象(交易引擎)
- _bd_mgr: 基础数据管理器
- _hot_mgr: 主力合约管理器

主要逻辑
1. 获取配置, 是否需要检查本地时间戳`_check_time`
2. 获取配置, 加载行情dll`module`
3. 根据行情dll创建行情api接口`_parser_api`
4. 获取配置`filter`, 检查订阅的交易所添加到`_exchg_filter`
5. 获取配置`code`, 检查订阅的品种添加到`_code_filter`
6. 行情api接口相关逻辑
    1. 将自己通过注册方式传递给行情api的`m_sink`
    2. 通过配置初始化行情api
    3. 将订阅的合约添加到订阅列表`contractSet`
    4. 将订阅的交易所包含的所有合约添加到订阅列表`contractSet`
    5. 通过行情api订阅`contractSet`品种行情

#### initExt
初始化执行器(不需要配置), 传入参数
- _id: 适配器id
- _parser_api: 行情api
- _stub: 数据落地对象(交易引擎)
- _bd_mgr: 基础数据管理器
- _hot_mgr: 主力合约管理器

主要逻辑:
1. 将自己通过注册方式传递给行情api的`m_sink`
2. 通过初始化行情api
3. 通过基础数据管理器获取合约列表并添加到订阅列表`contractSet`
4. 将订阅的交易所包含的所有合约添加到订阅列表`contractSet`
5. 通过行情api订阅`contractSet`品种行情

#### run
启动行情适配器, 只需启动行情api连接即可

#### handleSymbolList
处理合约列表, 适配器不做处理

#### handleQuote
处理实时行情, 实际通过行情api`ParserCTP::OnRtnDepthMarketData`回调

处理逻辑:
1. 检查数据是由有问题
2. 根据配置中的交易所过滤数据
3. 检查通过基础数据管理器是否能够获取合约信息
4. 检查数据和本地时间戳差异
5. 判断品种是商品期权, 主力/次主力合约还是普通合约
6. 将数据传递给交易引擎处理`_stub->handle_push_quote(quote, hotflag)`

#### handleOrderQueue
处理订单委托队列

处理逻辑:
1. 检查交易所过滤
2. 检查订单交易日
3. 检查合约信息
4. 将数据传给交易引擎处理`_stub->handle_push_order_queue(ordQueData)`

#### handleOrderDetail
处理逐笔委托数据

处理逻辑:
1. 检查交易所过滤
2. 检查订单交易日
3. 检查合约信息
4. 将数据传给交易引擎处理`_stub->handle_push_order_detail(ordDtlData)`

#### handleTransaction
处理逐笔成交数据

处理逻辑:
1. 检查交易所过滤
2. 检查订单交易日
3. 检查合约信息
4. 将数据传给交易引擎处理`_stub->handle_push_transaction(transData)`

#### handleParserLog
输出日志

## ParserAdapterMgr
适配器管理器, 主要负责同时管理多个适配器

#### run
启动管理器中所有的适配器

#### addAdapter
向管理器中添加适配器对象