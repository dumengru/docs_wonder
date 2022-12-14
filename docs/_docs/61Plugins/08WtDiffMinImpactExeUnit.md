---
title: WtDiffMinImpactExeUnit
category: Plugins
order: 8
---

## WtDiffMinImpactExeUnit
继承`ExecuteUnit`

#### init
根据"executers.yaml"中的`policy`初始化执行器

#### do_calc
1. 检查计算状态
2. 计算买卖轧平后的订单量`undone`(包括已发未成交)
3. 获取未执行差量`diffPos`
3. 如果上述二者有0则返回
4. 检查下单时间间隔
5. 通过`diffPos`判断`isBuy`是买入/卖出
6. 如果没有新tick, 则不操作
7. 根据配置计算下单量
8. 调整下单量: 有空单还需要买入, 或有多单还需要卖出
9. 根据配置价格类型计算委托价格
10. 检查涨跌停价
11. 通过`_ctx->buy`和`_ctx->sell`下单

#### on_order
1. `_orders_mon`找不到本地订单id`localid`直接返回
2. 如果订单被撤销, 更新撤单计数`_cancel_cnt`(有几笔撤单`_cancel_cnt`就是几)
3. 如果订单未被撤销, 并且剩余数量为0, 重置撤单次数`_cancel_times`(`_cancel_times`在下单时用作滑点倍数计算)
4. 如果订单被撤销需要重新计算

#### on_tick
1. 检查错误ticks
2. 保留新的tick
3. 如果设置了订单过期时间, 检查订单
4. 重新计算

#### on_trade
1. 更新订单差量`_left_diff`

#### on_entrust
1. 移除订单id
2. 重新计算

#### set_position
1. 更新最新差量`_left_diff`
2. 重新计算

#### clear_all_position
无操作

#### on_channel_ready
1. 获取未完成订单量`undone`
2. 如果`undone`不为0但, OMS为空, 撤消全部订单
3. 如果`undone`为0, 但OMS不为空, 清空OMS
4. 重新计算`do_calc`

#### on_channel_lost
无操作

