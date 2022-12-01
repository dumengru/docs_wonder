---
title: WtCtaEngine
category: CTA
order: 1
---

## WtCtaEngine
继承`WtEngine`, `IExecuterStub`

#### init
1. 回调父类`WtEngine::init`
2. 获取配置`_cfg`
3. 设置信号过滤器`_exec_mgr.set_filter_mgr`(hft没有, sel没有)

#### run
1. 创建ticker(跳动器)对象, 并初始化"config.yaml/env/product"
2. 策略数据落地"marker.json"
3. 回调跳动器`_tm_ticker->run`
4. 回调风险管理器`_risk_mon->self()->run`(hft没有, sel没有)

#### handle_push_quote
1. 行情适配器`ParserAdapter`传递过来tick数据
2. 回调跳动器`_tm_ticker->on_tick`

#### on_tick
1. 回调父类`WtEngine::on_tick`
2. 回调数据管理器`_data_mgr->handle_push_quote`
3. 判断该品种订阅了tick数据
4. 遍历品种订阅列表
5. 获取品种策略上下文管理器
6. 回调策略上下文管理器`ctx->on_tick`

#### on_bar
1. 遍历bar数据订阅列表
2. 获取品种策略上下文管理器
3. 回调策略上下文管理器`ctx->on_bar`

#### on_init
1. 清理执行器目标仓位数据缓存
2. 回调上下文管理`ctx->on_init`
3. 回调上下文管理`ctx->enum_position`

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
- isInTrading: 回调跳动器`_tm_ticker->is_in_trading`
- transTimeToMin: 回调跳动器`_tm_ticker->time_to_mins`
- get_comm_info: 回调基础数据管理器`_base_data_mgr->getCommodity`
- get_sess_info: 回调基础数据管理器`_base_data_mgr->getSession`

#### on_schedule(hft没有, sel没有)
1. 加载信号过滤器
2. 清空执行器目标仓位缓存
3. 获取上下文管理器, 回调`ctx->on_schedule`, 回调`ctx->enum_position`
4. 处理组合理论部位
5. 遍历品种持仓并更新持仓数据
6. 更新利润数据
7. 回调执行管理器`_exec_mgr.commit_cached_targets`
8. 保存数据
9. 回调事件监听器`_evt_listener->on_schedule_event`

#### handle_pos_change
(未完待续...)

#### addContext/getContext
添加/获取上下文管理器

#### addExecuter
添加执行器, 并将自己传递给执行器的`_stub`

#### loadRouterRules(hft没有, sel没有)
加载路由规则

