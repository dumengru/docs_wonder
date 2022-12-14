---
title: EventNotifier
category: Product_Common
order: 2
---

## EventNotifier
UDP广播对象

#### init
通过"notifier"初始化对象
1. 获取url
2. 加载dll"WtMsgQue.dll"
3. 获取创建服务端函数`_creator`
4. 获取删除服务端函数`_remover`
5. 获取发布消息函数`_publisher`
6. 获取注册回调函数`_register`
7. 注册消息回调函数`_register(on_mq_log)`
8. 创建MQServer`_mq_sid`
9. 启动一个异步对象`_asyncio`

#### notify
采用异步方式, 通过MQ发送交易消息

#### notifyLog
采用异步方式, 通过MQ发送日志消息

#### notifyEvent
采用异步方式, 通过MQ发送事件消息