---
title: WtSelEngine
category: SEL
order: 1
---

## WtSelEngine
继承`WtEngine`和`IExecuterStub`

#### init
1. 回调父类`WtEngine::init`
2. 获取配置`_cfg`

#### run
1. 创建ticker(跳动器)对象, 并初始化"config.yaml/env/product"
3. 策略数据落地"marker.json"
4. 回调跳动器`_tm_ticker->run`

#### handle_push_quote
1. 行情适配器`ParserAdapter`传递过来tick数据
2. 回调跳动器`_tm_ticker->on_tick`

#### on_tick
1. 回调父类`WtEngine::on_tick`
2. 回调数据管理器`_data_mgr->handle_push_quote`
3. 回调执行器`_exec_mgr.handle_tick`
4. 获取品种策略上下文管理器
5. 回调策略上下文管理器`ctx->on_tick`

#### on_bar
1. 遍历bar数据订阅列表
5. 获取品种策略上下文管理器
6. 回调策略上下文管理器`ctx->on_bar`

#### on_session_begin
1. 回调父类`WtEngine::on_session_begin`
2. 遍历策略上下文管理器
3. 回调策略上下文管理器`ctx->on_session_begin`
4. 回调事件监听器`_evt_listener->on_session_event`

#### on_session_end
1. 回调父类`WtEngine::on_session_end`
2. 遍历策略上下文管理器
3. 回调策略上下文管理器`ctx->on_session_end`
4. 回调事件监听器`_evt_listener->on_session_event`

#### 获取数据
- get_real_time: 获取当前时间
- transTimeToMin: 回调跳动器`_tm_ticker->time_to_mins`
- get_comm_info: 回调基础数据管理器`_base_data_mgr->getCommodity`
- get_sess_info: 回调基础数据管理器`_base_data_mgr->getSession`

#### on_minute_end
1. 判断日期是否跨夜
2. 遍历任务列表`_tasks`
3. (未完待续...)
4. 回调上下文管理器`ctx->on_schedule`


#### handle_pos_change
(未完待续...)

#### addContext/getContext
添加/获取上下文管理器

#### addExecuter
添加执行器, 并将自己传递给执行器的`_stub`

