---
title: HftStrategyMgr
category: Product_HFT
order: 5
---

## HftStraWrapper
封装一个策略
- _stra: 策略指针
- _fact: 策略工厂指针

## HftStrategyMgr
HFT策略管理器

#### loadFactories
1. 判断策略工厂文件是否存在
2. 获取创建策略工厂函数`creator`
3. 将策略工厂信息保存在`_factories`

#### createStrategy(const char* factname, const char* unitname, const char* id)
1. 获取策略工厂指针
2. 封装一个策略对象
3. 将策略指针保存在`_strategies`并返回策略指针

#### createStrategy(const char* name, const char* id)
1. 传入"config.yaml/strategies/hft"参数"name"和"id"
2. 获取策略工厂名称`factname`和策略名称`unitname`
3. 通过`factname`找到策略工厂信息
4. 创建策略指针保存在`_strategies`并返回策略指针

#### getStrategy
通过id获取策略指针
