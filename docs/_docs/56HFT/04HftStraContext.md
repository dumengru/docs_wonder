---
title: HftStraContext
category: Product_HFT
order: 4
---

## HftStraContext
策略上下文管理器, 继承`HftStraBaseCtx`

#### on_init
1. 回调父类`HftStraBaseCtx::on_init`
2. 回调策略`_strategy->on_init`

#### on_session_begin
1. 回调父类`HftStraBaseCtx::on_session_begin`
2. 回调策略`_strategy->on_session_begin`

#### on_session_end
1. 回调策略`_strategy->on_session_end`
2. 回调父类`HftStraBaseCtx::on_session_end`

#### on_tick
1. 更新利润数据
2. 回调策略`_strategy->on_tick`
3. 回调父类`HftStraBaseCtx::on_tick`

#### on_order_queue
1. 回调策略`_strategy->on_order_queue`
2. 回调父类`HftStraBaseCtx::on_order_queue`

#### on_order_detail
1. 回调策略`_strategy->on_order_detail`
2. 回调父类`HftStraBaseCtx::on_order_detail`

#### on_transaction
1. 回调策略`_strategy->on_transaction`
2. 回调父类`HftStraBaseCtx::on_transaction`

#### on_bar
1. 回调策略`_strategy->on_bar`
2. 回调父类`HftStraBaseCtx::on_bar`

#### on_trade
1. 回调策略`_strategy->on_trade`
2. 回调父类`HftStraBaseCtx::on_trade`

#### on_order
1. 回调策略`_strategy->on_order`
2. 回调父类`HftStraBaseCtx::on_order`


#### on_channel_ready
1. 回调策略`_strategy->on_channel_ready`
2. 回调父类`HftStraBaseCtx::on_channel_ready`

#### on_channel_lost
1. 回调策略`_strategy->on_channel_lost`
2. 回调父类`HftStraBaseCtx::on_channel_lost`

#### on_entrust
1. 回调策略`_strategy->on_entrust`
2. 回调父类`HftStraBaseCtx::on_entrust`

#### on_position
1. 回调策略`_strategy->on_position`

