---
title: CtaStraBaseCtx
category: Product_CTA
order: 3
---

## CtaStraBaseCtx
继承`ICtaStraCtx`(和hft有区别)

#### setTrader
设置交易适配器

#### id
获取策略上下文管理器id

#### on_init
1. 初始化数据输出模板
2. 加载资金, 仓位和信号数据(hft没有)
3. 加载用户数据

#### on_tick
1. 在`_price_map`中保存最新价
2. 检查交易信号
3. 调整持仓`do_set_position`
4. 如果是条件单触发, 回调`on_condition_triggered`
5. 更新浮动盈亏
6. 检查条件单
7. 回调`on_tick_updated`
8. 保存用户数据

#### on_bar
触发K线闭合, 回调`on_bar_close`

#### on_schedule
(未完待续...)

#### on_session_begin(hft没有)
每个交易日开始, 将冻结持仓置为零

#### on_session_end
1. 遍历品种持仓数据并更持仓新数据
2. 更新资金数据
3. 保存用户数据

---

> 策略接口(和hft区别很大)

#### stra_enter_long
1. 获取品种信息
2. 订阅tick数据`_engine->sub_tick`
3. 如果是市价单, 直接添加下单信号`append_signal`
4. 如果是限价单/停止单, 将交易条件添加到`_condtions`

#### stra_enter_short
1. 获取品种信息, 并判断是否可做空
2. 订阅tick数据`_engine->sub_tick`
3. 如果是市价单, 直接添加下单信号`append_signal`
4. 如果是限价单/停止单, 将交易条件添加到`_condtions`

#### stra_exit_long
1. 获取品种信息, 并判断可平仓位
2. 如果是市价单, 直接添加下单信号`append_signal`
3. 如果是限价单/停止单, 将交易条件添加到`_condtions`

#### stra_exit_short
1. 获取品种信息, 并判断可平仓位
2. 如果是市价单, 直接添加下单信号`append_signal`
3. 如果是限价单/停止单, 将交易条件添加到`_condtions`

#### stra_get_position
1. 获取持仓信息并调整持仓数据`_pos_map`

#### stra_set_position
1. 订阅tick数据`_engine->sub_tick`
2. 如果是市价单, 直接添加下单信号`append_signal`
3. 如果是限价单/停止单, 将交易条件添加到`_condtions`

#### stra_get_price
1. 通过`_price_map`获取价格, 找到即返回
2. 回调引擎`_engine->get_cur_price`

#### 通过引擎获取数据
- stra_get_day_price: 回调引擎`_engine->get_day_price`
- stra_get_tdate: 回调引擎`_engine->get_trading_date`
- stra_get_date: 回调引擎`_engine->get_date`
- stra_get_time: 回调引擎`_engine->get_min_time`
- stra_get_comminfo: 回调引擎`_engine->get_commodity_info`
- stra_get_last_tick: 回调引擎`_engine->get_last_tick`
- stra_get_ticks: 回调引擎`_engine->get_tick_slice`, 同时订阅tick
- stra_get_bars: 回调引擎`_engine->get_kline_slice`, 同时会判断K线闭合和订阅tick
- stra_get_rawcode: 回调引擎`_engine->get_rawcode`
- stra_sub_ticks: 回调引擎`_engine->sub_tick`, 同时将品种添加到订阅列表`_tick_subs`

#### 通过持仓信息获取数据
- stra_get_first_entertime: 从`_pos_map`获取首次入场时间
- stra_get_last_entertime: 从`_pos_map`获取最后一次入场时间
- stra_get_last_exittime: 从`_pos_map`获取最后一次离场时间
- stra_get_last_enterprice: 从`_pos_map`获取最后一次入场价
- stra_get_position_avgpx: 从`_pos_map`获取持仓数据计算平均利润
- stra_get_position_profit: 从`_pos_map`获取利润
- stra_get_detail_entertime: 从`_pos_map`获取品种开仓时间
- stra_get_detail_cost: 从`_pos_map`获取品种开仓价格
- stra_get_detail_profit: 从`_pos_map`获取品种当前利润
- stra_get_last_entertag: 从`_pos_map`获取最后一次入场标记

#### stra_get_fund_data
从`_fund_info`获取资金数据