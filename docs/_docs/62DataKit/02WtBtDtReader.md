---
title: WtBtDtReader
category: DataKit
order: 2
---

## WtBtDtReader

#### init
1. 传入"config.yaml"中的"store"或"path"
2. 将`HisDataMgr`传递给`_sink`
3. 获取数据路径`_base_dir`

#### read_raw_bars
读取"_base_dir/his/.../.dsb"中的bar数据文件

#### read_raw_ticks
读取"_base_dir/his/ticks/exchg/.../.dsb"中的tick数据文件



