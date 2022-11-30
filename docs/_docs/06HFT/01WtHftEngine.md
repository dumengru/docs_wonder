---
title: WtHftEngine
category: HFT
order: 1
---

## WtHftEngine
HFT策略引擎

#### 获取数据 
- get_order_queue_slice: 通过数据管理器获取委托队列数据
- get_order_detail_slice: 通过数据管理器获取逐笔委托数据
- get_transaction_slice: 通过数据管理器获取逐笔成交数据

#### 订阅数据
- sub_order_queue: 添加委托队列品种到`_ordque_sub_map`
- sub_order_detail: 添加委托明细品种到`_orddtl_sub_map`
- sub_transaction: 添加成交明细品种到`_trans_sub_map`

#### on_minute_end
功能已去除

#### addContext
添加上下文管理器

---

> WtEngine接口

#### init
1. 父类初始化`WtEngine::init`
2. 获取配置`_cfg`

#### run
1. 遍历策略上下文管理器, 并回调`ctx->on_init`
2. 创建ticker(暂且叫跳动器)对象, 并初始化"config.yaml/env/product"
3. 策略数据落地"marker.json"
4. 回调跳动器`_tm_ticker->run`

#### handle_push_quote
1. 行情适配器`ParserAdapter`传递过来tick数据
2. 回调跳动器`_tm_ticker->on_tick`

#### handle_push_order_detail
1. 行情适配器`ParserAdapter`传递过来逐笔委托数据
2. 获取品种委托明细
3. 遍历策略订阅列表
4. 获取策略上下文管理器, 回调`ctx->on_order_detail`

#### handle_push_order_queue
1. 行情适配器`ParserAdapter`传递过来委托队列数据
2. 获取品种委托队列
3. 遍历策略订阅列表
4. 获取策略上下文管理器, 回调`ctx->on_order_queue`

#### handle_push_transaction
1. 行情适配器`ParserAdapter`传递过来逐笔成交数据
2. 获取品种成交明细
3. 遍历策略订阅列表
4. 获取策略上下文管理器, 回调`ctx->on_transaction`

#### on_tick
1. 回调父类`WtEngine::on_tick`
2. 回调数据管理器`_data_mgr->handle_push_quote`
3. 判断该品种订阅了tick数据
4. 遍历品种订阅列表
5. 获取品种策略上下文管理器
6. 回调策略上下文管理器`ctx->on_tick`

#### on_bar
1. 遍历bar数据订阅列表
5. 获取品种策略上下文管理器
6. 回调策略上下文管理器`ctx->on_tick`

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
