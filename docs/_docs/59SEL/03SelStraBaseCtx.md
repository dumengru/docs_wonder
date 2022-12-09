---
title: SelStraBaseCtx
category: SEL
order: 3
---

## SelStraBaseCtx
继承`SelStraBaseCtx`

#### on_init
1. 初始化数据输出模板
2. 加载资金, 仓位和信号数据
3. 加载用户数据

#### on_session_begin(hft没有)
每个交易日开始, 将冻结持仓置为零

#### on_session_end
1. 遍历品种持仓数据并更持仓新数据
2. 更新资金数据
3. 保存用户数据

#### on_tick
1. 在`_price_map`中保存最新价
2. 检查交易信号
3. 调整持仓`do_set_position`
4. 更新浮动盈亏
5. 回调`on_tick_updated`
6. 保存用户数据

#### on_bar
触发K线闭合, 回调`on_bar_close`

#### on_schedule
(未完待续...)

#### stra_get_position
获取持仓信息并调整持仓数据`_pos_map`

#### stra_set_position
1. 获取品种信息
2. 判断品种是否可做空
3. 判断目标仓位和当前仓位是否一致
4. 判断品种是否T+1操作
5. 添加信号`append_signal`

#### stra_get_price
1. 通过`_price_map`获取价格, 找到即返回
2. 回调引擎`_engine->get_cur_price`

#### 通过引擎获取数据
- stra_get_date: 获取调度日期`_schedule_date`或`_engine->get_date`
- stra_get_time: 获取调度时间`_schedule_time`或`_engine->get_min_time`
- stra_get_comminfo: 回调引擎`_engine->get_commodity_info`
- stra_get_rawcode: 回调引擎`_engine->get_rawcode`
- stra_get_sessinfo: 回调引擎`_engine->get_session_info`
- stra_sub_ticks: 回调引擎`_engine->sub_tick`, 并将订阅品种存放在`_tick_subs`
- stra_get_last_tick: 回调引擎`_engine->get_last_tick`
- stra_get_ticks: 回调引擎`_engine->get_tick_slice`
- stra_get_bars: 回调引擎`_engine->get_kline_slice`
