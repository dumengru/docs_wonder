---
title: 执行器exec
category: 回测进阶
order: 4
---

## ExecMocker
执行器, 继承`ExecuteContext`, `IDataSink`, `IMatchSink`

构造时传入回测引擎`_replayer`

#### init
通过"configbt.yaml"中的`exec`初始化, 执行的算法是`executer/name`

#### handle_init
回测前准备
1. 回调回测引擎获取K线数据`_replayer->get_kline_slice`
2. 回调回测引擎订阅tick`_replayer->sub_tick`
3. 回调算法执行单元`_exec_unit->on_channel_ready`
4. 回调算法执行单元设置目标仓位`_exec_unit->set_position`

#### handle_schedule
K线闭合回调
1. 如果是当天最后一根K线`1500`, 直接返回
2. 获取tick最新价`_sig_px`
3. 根据配置`_volmode`设置目标仓位`_target`
4. 回调执行单元设置仓位`_exec_unit->set_position`

#### handle_replay_done
数据回放完毕回调
1. 创建目录"exec/"
2. 保存交易数据到"trades_id.csv"

#### handle_order
回调执行单元`_exec_unit->on_order`

#### handle_trade
回调执行单元`_exec_unit->on_trade`

#### handle_entrust
回调执行单元`_exec_unit->on_entrust`
