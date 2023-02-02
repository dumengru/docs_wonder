---
title: DataManager
category: DataKit
order: 1
---

## DataManager
继承`IDataWriterSink`

#### init
1. 传入
- 配置"dtcfg.yaml"中的"writer"
- 基础数据管理器`_bd_mgr`
- 状态机`_state_mon`
- UPD广播`_udp_caster`
2. 创建数据写入器并初始化`_writer->init`

#### add_ext_dumper
向数据写入器中添加数据保存器`_writer->add_ext_dumper`

#### writeTick
回调`_writer->writeTick`

#### writeOrderQueue
回调`_writer->writeOrderQueue`

#### writeOrderDetail
回调`_writer->writeOrderDetail`

#### writeTransaction
回调`_writer->writeTransaction`

#### transHisData
回调`_writer->transHisData`

#### isSessionProceeded
回调`_writer->isSessionProceeded`

#### getCurTick
回调`_writer->getCurTick`

--- 
**IDataWriterSink**

#### canSessionReceive
回调`_state_mon->isInState`

#### broadcastTick
回调`_udp_caster->broadcast`

#### broadcastOrdQue
回调`_udp_caster->broadcast`

#### broadcastOrdDtl
回调`_udp_caster->broadcast`

#### broadcastOrdDtl
回调`_udp_caster->broadcast`

#### broadcastTrans
回调`_udp_caster->broadcast`
