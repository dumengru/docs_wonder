---
title: WtCtaTicker
category: CTA
order: 2
---

## WtCtaRtTicker
cta跳动器

#### init
1. 保存数据读取器`_store`
2. 获取品种交易时间`_s_info`

#### on_tick
1. 通过引擎传递过来的tick数据
2. 如果线程为空, 触发`trigger_price`并返回
3. 如果行情时间小于本地时间, 触发`trigger_price`并返回
4. 时间校验(未完待续...)
5. 如果分钟结束
    1. 回调数据读取器`_store->onMinuteEnd`
    2. 回调策略引擎`_engine->on_schedule`
    3. 回调策略引擎`_engine->on_session_end`
6. 触发`trigger_price`

#### trigger_price
1. 回调引擎`_engine->on_tick`
2. 回调主力合约引擎`_engine->on_tick`

#### run
1. 通过交易引擎设置交易日
2. 回调引擎`_engine->on_init`
3. 回调引擎`_engine->on_session_begin`
4. 启动线程
    1. 时间校验(未完待续...)
    2. 回调数据读取器`_store->onMinuteEnd`
    3. 回调引擎`_engine->on_schedule`(hft没有, sel没有)
    4. 回调引擎`_engine->on_session_end`

#### stop
1. 停止线程
