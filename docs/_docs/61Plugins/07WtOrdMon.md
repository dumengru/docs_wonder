---
title: WtOrdMon
category: Plugins
order: 7
---

## WtOrdMon
订单管理器

#### push_order
向订单列表中添加一笔订单

#### erase_order
删除传入id的订单

#### has_order
通过id判断是否有订单

#### check_orders
检查订单
1. 判断订单列表是否为空
2. 遍历订单列表
3. 判断是否可撤单
4. 判断订单是否过期
5. 通过回调函数处理订单

#### clear_orders
清空订单列表

