---
title: WtExecuterFactory
category: Exec
order: 5
---

## ExeUnitWrapper
封装一个执行单元
- 执行单元指针
- 执行单元工厂

## WtExecuterFactory

#### loadFactories
1. 判断执行单元工厂文件是否存在
2. 获取创建执行单元工厂函数`creator`
3. 将执行单元工厂信息保存在`_factories`

#### createExeUnit/createDiffExeUnit(const char* factname, const char* unitname)
1. 获取执行单元工厂指针
2. 创建一个执行单元指针
3. 返回封装的执行单元指针

#### createExeUnit/createDiffExeUnit(const char* name)
1. 传入"executers.yaml/executers/policy"中的配置
2. 获取执行单元工厂名称`factname`和策略名称`unitname`
3. 创建执行单元指针
4. 封装执行单元指针并返回
