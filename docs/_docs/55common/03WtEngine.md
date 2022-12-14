---
title: WtEngine
category: Product_Common
order: 1
---

## WtRiskMonWrapper
风控接口

## IEngineEvtListener 
引擎事件监听接口

## WtEngine
策略引擎

#### 设置数据
- set_adapter_mgr: 设置交易适配器
- set_date_time: 设置日期时间
- set_trading_date: 设置当前交易日
- setRiskMonitor: 设置风控对象`_risk_mon`
- regEventListener: 设置事件监听对象`_evt_listener`

#### 获取数据
- get_basedata_mgr: 获取基础数据管理器
- get_hot_mgr: 获取主力合约管理器
- get_session_info: 获取合约交易时间
- get_commodity_info: 获取商品信息
- get_contract_info: 获取合约信息
- get_rawcode: 获取合约标准码
- get_last_tick: 通过基础数据管理器获取最新价
- get_tick_slice: 通过基础数据管理器获取tick数据切片
- get_kline_slice
    1. 获取商品信息
    2. 获取K线数据订阅表
    3. 通过基础数据管理器获取K线切片数据
- sub_tick:
    1. (未完待续...)
- get_cur_price: 
    1. 通过_price_map获取品种价格
    2. 若找不到, 通过数据管理器`_data_mgr`获取合约价格
- get_day_price: 
    1. 通过数据管理器`_data_mgr`获取合约价格
    2. 通过flag参数返回对应价格
    - "0": "open"
    - "1": "high"
    - "2": "low"
    - "3": "close"
- get_exright_factor: 获取复权因子
- get_adjusting_flag: 通过数据管理器获取复权标记

#### calc_fee
1. 获取品种标准码
2. 通过手续费映射`_fee_map`查询品种手续费

3. 获取品种信息
4. 获取手续费模板
5. 计算手续费

---

> WtPortContext接口

#### getFundInfo
1. 更新资金信息
2. 保存数据

#### setVolScale
调整风控规模

#### writeRiskLog
输出风控日志

#### 获取数据
- getCurDate: 获取当前日期
- getCurTime: 获取当前时间
- getTradingDate: 获取当前交易日

--- 

> IParserStub接口

#### handle_push_quote
处理tick数据推送
1. 回调数据管理器`_data_mgr->handle_push_quote`
2. 回调引擎`on_tick`
3. 如果是主力合约, 回调主力合约`data_mgr->handle_push_quote`和`on_tick`
4. 如果是次主力合约, 回调次主力合约`data_mgr->handle_push_quote`和`on_tick`

#### init
1. 初始化组件
- `_base_data_mgr`: 基础数据管理器
- `_data_mgr`: 数据管理器
- `_hot_mgr`: 主力合约管理器
- `_notifier`: UDP广播对象
- `_filter_mgr`: 信号过滤器
2. 加载费用
3. 加载资金, 仓位, 风控数据
4. 初始化数据输出模板: "trades.csv"和"closes.csv"
5. 初始化风控模块

#### on_tick
on_tick回调
1. 在`_price_map`中保存最新价
2. 检查信号是否触发
3. 如果成交量为0直接返回(这个逻辑对嘛?如果订单簿发生了变化呢)
4. 获取持仓信息
5. 更新保存持仓数据

#### on_session_begin
无操作

#### on_session_end
保存资金结算数据"funds.csv"

#### 需子类实现接口
- run
- on_bar
- on_init
