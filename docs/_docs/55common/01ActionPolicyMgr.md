---
title: ActionPolicyMgr
category: common
order: 1
---

## ActionPolicyMgr
开平规则管理器

#### init
1. 加载`actpolicy.yaml`配置
2. 遍历开平规则`order`
- action类别: open/close/closetoday/closeyestoday
- limit: 开仓限制
- limit_s: 做空限制
- limit_l: 做多限制
3. 遍历品种`filters`

#### getActionRules
通过品种找到对平开平规则组, 如果找不到, 则使用默认开平规则