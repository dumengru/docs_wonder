---
title: SelStraContext
category: Product_SEL
order: 4
---

## SelStraContext
继承`SelStraBaseCtx` 

#### on_init
1. 回调父类`SelStraBaseCtx::on_init`
2. 回调策略`_strategy->on_init`

#### on_session_begin
1. 回调父类`SelStraBaseCtx::on_session_begin`
2. 回调策略`_strategy->on_session_begin`

#### on_session_end
1. 回调策略`_strategy->on_session_end`
2. 回调父类`SelStraBaseCtx::on_session_end`

#### on_tick_updated
回调策略`_strategy->on_tick`

#### on_bar_close
回调策略`_strategy->on_bar_close`

#### on_strategy_schedule
回调策略`_strategy->on_schedule`