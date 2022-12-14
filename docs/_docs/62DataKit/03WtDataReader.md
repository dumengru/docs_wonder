---
title: WtDataReader
category: DataKit
order: 3
---

## WtDataReader
数据读取器, 类中定义各种数据结构体及相互转换比较凌乱, 因此略过相关细节

#### init
1. 通过sink(`DataManager`)获取
- `_base_data_mgr`
- `_hot_mgr`
2. 获取数据文件目录"rt/"和"his/"
3. 加载除权因子

#### onMinuteEnd
1. 检查时间戳是否异常
2. 遍历`_bars_cache`, 处理完K线后回调`_sink->on_bar`
3. 全部处理完后回调`_sink->on_all_bar_updated`

#### readTickSlice
1. 获取品种完整ID
2. 如果传入`etim`, 则获取`etime`对应时间戳; 否则获取最新时间戳
3. 判断最后交易日是否是今天`isToday`
4. 如果是期货品种, 获取对应期货合约代码`curCode`
5. 中间处理(略)
6. 创建tick数据切片`WTSTickSlice::create`

#### readOrdDtlSlice
逻辑同`readTickSlice`

#### readOrdQueSlice
逻辑同`readTickSlice`

#### readTransSlice
逻辑同`readTickSlice`

#### readKlineSlice
略