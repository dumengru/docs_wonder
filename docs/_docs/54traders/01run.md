---
title: run
category: Traders
order: 1
---

## 流程回顾
在"RunnerHft"仿真测试中, 能够看到, 程序启动的入口在"WtRunner.cpp"文件下的`WtRunner::run"方法中

```cpp
void WtRunner::run(bool bAsync /* = false */)
{
	try
	{
        // 启动行情适配管理器
		_parsers.run();
        // 启动交易适配管理器
		_traders.run();
        // 启动交易引擎
		_engine->run(bAsync);
	}
}
```

其中交易适配管理器的初始化在`WtRunner::initTraders`方法中

```cpp
bool WtRunner::initTraders(WTSVariant* cfgTrader)
{
	if (cfgTrader == NULL || cfgTrader->type() != WTSVariant::VT_Array)
		return false;
	
	uint32_t count = 0;
	for (uint32_t idx = 0; idx < cfgTrader->size(); idx++)
	{
        // 1. 获取"tdtraders.yaml"中的交易配置
		WTSVariant* cfgItem = cfgTrader->get(idx);
		if (!cfgItem->getBoolean("active"))
			continue;

		const char* id = cfgItem->getCString("id");
        // 2. 创建交易适配器, 并初始化
		TraderAdapterPtr adapter(new TraderAdapter(&_notifier));
		adapter->init(id, cfgItem, &_bd_mgr, &_act_policy);
        // 3. 将交易适配器添加到交易管理器
		_traders.addAdapter(id, adapter);

		count++;
	}

	WTSLogger::info("{} traders loaded", count);

	return true;
}
```

## 底层逻辑
因此WonderTrader对交易接口的管理是这样的: 交易接口(TraderCTP) -> 行情适配器(TraderAdapter) -> 行情适配管理器(TraderAdapterMgr)
