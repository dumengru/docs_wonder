---
title: WtDistExecuter
category: Product_Exec
order: 2
---

## WtDistExecuter
继承`IExecCommand`

#### init
1. 获取配置参数

#### set_position
1. 遍历目标仓位`targets`
2. 获取合约代码
3. 获取交易量
4. 计算目标仓位`newVol *= _scale`
5. 将调整数据保存在`_target_pos`

#### on_position_changed
调整仓位变动
1. 计算目标仓位`targetPos *= _scale`
2. 将调整数据保存在`_target_pos`

#### on_tick
无操作