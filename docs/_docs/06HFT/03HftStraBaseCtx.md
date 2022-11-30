---
title: HftStraBaseCtx
category: HFT
order: 3
---

## HftStraBaseCtx
继承`IHftStraCtx`和`ITrdNotifySink`

#### setTrader
设置交易适配器

#### id
获取策略上下文管理器id

#### on_init
1. 初始化数据输出模板
2. 加载用户数据

#### on_tick
保存用户数据

#### on_order_queue/on_order_detail/on_transaction/on_bar
1. 通过引擎回调策略上下文管理器
2. 保存用户数据

#### on_session_begin
无操作

#### on_session_end
遍历品种持仓数据并更新

#### stra_cancel
回调交易适配器`_trader->cancel`

#### 下单函数
- stra_cancel: 通过调用`_trader->cancel`撤单
- stra_buy: 通过调用`_trader->buy`买入
- stra_sell: 通过调用`_trader->sell`卖出
- stra_enter_long: 通过调用`_trader->openLong`开仓多单
- stra_enter_short: 通过调用`_trader->openShort`开仓空单
- stra_exit_long: 通过调用`_trader->closeLong`平仓多单
- stra_exit_short: 通过调用`_trader->closeShort`平仓空单

#### 通过引擎获取数据
- stra_get_comminfo: 通过引擎获取品种信息
- stra_get_bars: 回调引擎`_engine->get_kline_slice`并订阅品种tick数据
- stra_get_ticks: 回调引擎`_engine->get_tick_slice`并订阅品种tick数据
- stra_get_order_detail: 回调引擎`_engine->get_order_detail_slice`, 并订阅`_engine->sub_order_detail`
- stra_get_order_queue: 回调引擎`_engine->get_order_queue_slice`, 并订阅`_engine->sub_order_queue`
- stra_get_transaction: 回调引擎`_engine->get_transaction_slice`, 并订阅`_engine->sub_transaction`
- stra_get_last_tick: 回调引擎`_engine->get_last_tick`
- stra_get_rawcode: 回调引擎`_engine->get_rawcode`
- stra_get_date: 回调引擎`_engine->get_date`
- stra_get_time: 回调引擎`_engine->get_raw_time`
- stra_get_secs: 回调引擎`_engine->get_secs`

#### 通过引擎订阅数据
- stra_sub_ticks: 订阅品种添加到`_tick_subs`, 回调引擎`_engine->sub_tick`
- stra_sub_order_details: 回调引擎`_engine->sub_order_detail`
- stra_sub_order_queues: 回调引擎`_engine->sub_order_queue`
- stra_sub_transactions: 回调引擎`_engine->sub_transaction`

#### 通过交易适配器获取数据
- stra_get_position: 回调适配器`_trader->getPosition`
- stra_get_undone: 回调适配器`_trader->getUndoneQty`

#### 其他方式获取数据
- stra_get_position_avgpx: 从`_pos_map`获取持仓数据计算平均利润
- stra_get_position_profit: 从`_pos_map`获取利润
- stra_get_price
    1. 通过`_price_map`获取价格, 找到即返回
    2. 回调引擎`_engine->get_cur_price`

#### 策略回调函数
- on_trade
    1. 保存用户数据
    2. 如果有信号, 输出信号
    3. 调整持仓
- on_order: 保存用户数据
- on_channel_ready: 保存用户数据
- on_channel_lost: 保存用户数据
- on_entrust: 保存用户数据
- on_position: 无操作
