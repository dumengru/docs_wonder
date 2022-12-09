---
title: WtExecMgr
category: Exec
order: 6
---

## WtExecuterMgr
执行管理器, 主要负责管理多个执行器

#### set_filter_mgr
设置过滤器

#### add_executer
添加执行器

#### enum_executer
枚举执行器

#### set_positions
设置目标持仓
(未完待续...)
1. 回调执行器`executer->set_position`

#### handle_pos_change
1. 回调执行器`executer->on_position_changed`

#### handle_tick
1. 回调执行器`executer->on_tick`

#### load_router_rules/get_route
加载/获取路由规则(未完待续...)

#### add_target_to_cache
1. 添加缓存目标仓位

#### clear_cached_targets
1. 清除缓存目标仓位

#### commit_cached_targets
1. 遍历所有品种目标仓位
2. 对组合进行缩放
3. 根据过滤器调整目标仓位
4. 遍历执行器并回调`executer->set_position`
5. 清除缓存的目标仓位
