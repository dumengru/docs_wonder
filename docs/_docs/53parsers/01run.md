---
title: run
category: parsers
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

其中行情适配管理器的初始化在`WtRunner::initParsers`方法中

```cpp
bool WtRunner::initParsers(WTSVariant* cfgParser)
{
	if (cfgParser == NULL)
		return false;

	uint32_t count = 0;
	for (uint32_t idx = 0; idx < cfgParser->size(); idx++)
	{
        // 获取"tdparsers.yaml"中的行情配置
		WTSVariant* cfgItem = cfgParser->get(idx);
		if(!cfgItem->getBoolean("active"))
			continue;

		const char* id = cfgItem->getCString("id");
		// By Wesley @ 2021.12.14
		// 如果id为空，则生成自动id
		std::string realid = id;
		if (realid.empty())
		{
			static uint32_t auto_parserid = 1000;
			realid = StrUtil::printf("auto_parser_%u", auto_parserid++);
		}
        // 创建行情适配器并初始化
		ParserAdapterPtr adapter(new ParserAdapter);
		adapter->init(realid.c_str(), cfgItem, _engine, &_bd_mgr, &_hot_mgr);
        // 将初始化完成的行情适配器添加到管理器中
		_parsers.addAdapter(realid.c_str(), adapter);

		count++;
	}

	WTSLogger::info("{} parsers loaded", count);
	return true;
}
```

## 底层逻辑
因此WonderTrader对行情接口的管理是这样的: 行情接口(ParserCTP) -> 行情适配器(ParserAdapter) -> 行情适配管理器(ParserAdapterMgr)