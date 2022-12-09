---
title: WtTWapExeUnit
category: Plugins
order: 10
---

## WtTWapExeUnit
继承`ExecuteUnit`

#### init
根据"executers.yaml"中的`policy`初始化执行器

#### do_calc
1. 判断交易通道是否就绪
2. 如果有正在撤单, 不能继续计算
3. 计算买卖轧平后的订单量`undone`(包括已发未成交)
4. 如果有未完成订单, 直接返回
5. 计算未执行差量`diffQty`
6. 计算本轮目标仓位
7. 根据配置价格类型计算委托价格
8. 通过`_ctx->buy`和`_ctx->sell`下单

#### on_order
1. `_orders_mon`找不到本地订单id`localid`直接返回
2. 如果订单被撤销, 更新撤单计数`_cancel_cnt`(有几笔撤单`_cancel_cnt`就是几)
3. 如果订单未被撤销, 并且剩余数量为0, 重置撤单次数`_cancel_times`(`_cancel_times`在下单时用作滑点倍数计算)
4. 如果订单被撤销需要重新计算

#### on_tick
1. 检查错误ticks
2. 保留新的tick
3. 如果是第一个tick, 检查目标仓位不一致要重新计算
4. 检查订单
5. 重新计算

#### on_trade
无操作

#### on_entrust
1. 移除订单id
2. 重新计算

#### set_position
1. 更新目标仓位`_target_pos`
2. 重置已执行次数`_fired_times`
3. 重新计算

#### on_channel_ready
1. 获取未完成订单量`undone`
2. 如果`undone`不为0但, OMS为空, 撤消全部订单
3. 重新计算`do_calc`

#### on_channel_lost
无操作