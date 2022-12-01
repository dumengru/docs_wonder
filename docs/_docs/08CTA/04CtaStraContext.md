---
title: CtaStraContext
category: CTA
order: 4
---

## CtaStraContext
继承`CtaStraBaseCtx` 

#### on_init
1. 回调父类`CtaStraBaseCtx::on_init`
2. 回调策略`_strategy->on_init`

#### on_session_begin
1. 回调父类`CtaStraBaseCtx::on_session_begin`
2. 回调策略`_strategy->on_session_begin`

#### on_session_end
1. 回调策略`_strategy->on_session_end`
2. 回调父类`CtaStraBaseCtx::on_session_end`

#### on_tick_updated
回调策略`_strategy->on_tick`

#### on_bar_close
回调策略`_strategy->on_bar_close`

#### on_calculate
回调策略`_strategy->on_schedule`

#### on_condition_triggered
回调策略`_strategy->on_condition_triggered`
