---
title: WtLocalExecuter
category: Exec
order: 2
---

## WtLocalExecuter
本地执行器, 继承`ExecuteContext`, `ITrdNotifySink`, `IExecCommand`

#### init
1. 传入`executers.yaml`参数
2. 获取参数
- _scale: 数量放大倍数，即该执行器的目标仓位，是组合理论目标仓位的多少倍，可以为小数
- _strict_sync: 是否开启严格同步
- poolsize: 开启线程数量
- 
- clear: 过期主力自动清理配置
- group: 

#### setTrader
设置交易适配器

#### getUnit
1. 获取品种名称
2. 获取执行单元分配策略设置`policy`
3. 若`_unit_map`中存在执行单元直接返回
4. 创建执行单元并初始化, 返回执行单元

---

> ExecuteContext接口

#### 通过数据管理器获取数据
- getTicks: 回调数据管理器`_data_mgr->get_tick_slice`
- grabLastTick: 回调数据管理器`_data_mgr->grab_last_tick`

#### 通过交易适配器获取数据
- getPosition: 回调适配器`_trader->getPosition`
- getUndoneQty: 回调适配器`_trader->getUndoneQty`
- getOrders: 回调适配器`_trader->getOrders`
- buy: 回调适配器`_trader->buy`
- sell: 回调适配器`_trader->sell`
- cancel: 回调适配器`_trader->cancel`

#### writeLog
输出执行器日志

#### 通过策略引擎获取数据
`_stub`就是策略引擎
- getCommodityInfo: 回调引擎`_stub->get_comm_info` 
- getSessionInfo: 回调引擎`_stub->get_sess_info`
- getCurTime: 回调引擎_stub->get_real_time`

#### set_position
设置目标仓位
(未完待续...)

#### on_position
(未完待续...)

#### 回调执行单元
- on_position_changed: `unit->self()->set_position`
- on_tick: `unit->self()->on_tick`
- on_trade: `unit->self()->on_trade`
- on_order: `unit->self()->on_order`
- on_entrust: `unit->self()->on_entrust`
- on_channel_ready: `unitPtr->self()->on_channel_ready`
- on_channel_lost: `unitPtr->self()->on_channel_lost`
- on_account: `unitPtr->self()->on_account`