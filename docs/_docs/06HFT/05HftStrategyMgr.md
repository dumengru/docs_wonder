---
title: HftStrategyMgr
category: HFT
order: 5
---

## HftStraWrapper
包装一个策略
- _stra: 策略指针
- _fact: 策略工厂指针

## HftStrategyMgr
HFT策略管理器

#### loadFactories
1. 判断策略工厂文件是否存在
2. 获取创建策略工厂函数`creator`
3. 将策略工厂信息保存在`_factories`

#### createStrategy
1. 获取策略工厂指针
2. 包装一个策略对象
3. 将策略指针保存在`_strategies`

#### getStrategy
通过id获取策略指针