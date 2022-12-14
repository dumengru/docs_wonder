---
title: WtDtMgr
category: Product_Datas
order: 1
---

## WtDtMgr
继承`IDataManager`和`IDataReaderSink`

#### init
1. 传入"config.yaml"中的"data"
2. 将策略引擎传递给`_engine`

#### initStore
1. 传入"config.yaml"中的"data/store"
2. 默认加载"WtDataStorage.dll"读取数据
3. 创建数据读取器`_reader`
4. 利用自己初始化数据读取器`_reader->init`

#### regsiter_loader
添加历史数据加载器`_loader`

#### handle_push_quote
处理收到的tick数据
1. 将tick数据添加到实时tick缓存`_rt_tick_map`
2. 如果有后复权, 将后复权tick添加到`tData`

---

**IDataManager接口**

#### get_tick_slice
获取tick数据切片
1. 如果不是后复权, 直接回调数据读取器`_reader->readTickSlice`
2. 后复权处理(略)

#### get_order_queue_slice
回调数据读取器`_reader->readOrdQueSlice`

#### get_order_detail_slice
回调数据读取器`_reader->readOrdDtlSlice`

#### get_transaction_slice
回调数据读取器`_reader->readTransSlice`

#### get_kline_slice
1. 基础周期数据直接回调数据读取器`_reader->readKlineSlice`
2. 非基础周期数据处理(略)

#### grab_last_tick
回调实时tick缓存`_rt_tick_map->get`

#### get_adjusting_factor
回调数据读取器`_reader->getAdjFactorByDate`

#### get_adjusting_flag
回调数据读取器`_reader->getAdjustingFlag`

--- 

**IDataReaderSink**

#### on_bar
每个品种形成bar之后回调
1. 构造品种周期名称`key_pattern`
2. 如果是基础周期, 直接将品种信息添加到`_bar_notifies`
3. 非基础周期处理(略)

#### on_all_bar_updated
所有品种形成bar之后回调
1. 遍历`_bar_notifies`
2. 回调引擎`_engine->on_bar`

#### get_basedata_mgr
回调引擎`_engine->get_basedata_mgr`

#### get_hot_mgr
回调引擎`_engine->get_hot_mgr`

#### get_date
回调引擎`_engine->get_date`

#### get_min_time
回调引擎`_engine->get_min_time`

#### get_secs
回调引擎`_engine->get_secs`
