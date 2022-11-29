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

#### 获取数据
- stra_get_comminfo
- stra_get_bars
- stra_get_ticks
- stra_get_order_detail
- stra_get_order_queue
- stra_get_transaction
- stra_get_last_tick
- stra_get_rawcode

#### 


#### 


#### 


#### 



#### 


#### 


#### 


#### 


#### 


#### 


#### 