---
title: Incs
category: common
order: 4
---


## 简介
在目录"Product/WtCore/Incs"中的文件, 主要用来定义各类接口

#### RiskMonDefs
1. WtPortContext: 风控组合环境
2. WtRiskMonitor: 组合风控模块
3. IRiskMonitorFact: 风控模块工厂
4. 定义函数
- FuncCreateRiskMonFact: 创建执行工厂
- FuncDeleteRiskMonFact: 删除执行工厂

#### ITrdNotifySink
1. ITrdNotifySink

#### IDataReader
1. IDataReaderSink: 数据读取模块向调用模块回调
2. IHisDataLoader: 历史数据加载器
3. IDataReader: 数据读取
4. 定义函数
- FuncCreateDataReader: 创建数据读取对象
- FuncDeleteDataReader: 删除数据读取对象

#### IHftStraCtx
1. IHftStraCtx: Hft策略环境

#### HftStrategyDefs
1. HftStrategy: Hft策略
2. IHftStrategyFact: Hft策略工厂
3. 定义函数
- FuncCreateHftStraFact: 创建执行工厂
- FuncDeleteHftStraFact: 删除执行工厂

#### ExecuteDefs
1. ExecuteContext: 执行环境
2. ExecuteUnit: 执行器
3. IExecuterFact: 执行器工厂
4. 定义函数
- FuncCreateExeFact: 创建执行工厂
- FuncDeleteExeFact: 删除执行工厂

#### ICtaStraCtx
1. ICtaStraCtx: Cta策略环境

#### CtaStrategyDefs
1. CtaStrategy: Cta策略
2. ICtaStrategyFact: Cta策略工厂
3. 定义函数
- FuncCreateStraFact: 创建执行工厂
- FuncDeleteStraFact: 删除执行工厂

#### ISelStraCtx
1. ISelStraCtx: Sel策略环境