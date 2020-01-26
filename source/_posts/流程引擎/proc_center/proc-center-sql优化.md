---
title: proc-center-sql优化.md
date: 2019-12-20 16:13:27
categories: 
- [数据库]
tags: 
- 持续更新
- 流程中心
---

> 前段时间写了一个流程中心，因时间紧张且上线初期数据不多，没有过多关注性能优化，现在准备逐步优化
目标支撑1千万的数据量原测试代码在10秒内跑完。  
记录优化过程。
<!--more-->

```sql
create index ACT_HI_TASK_USER_SYS_ID_USER_ID_index
	on ACT_HI_TASK_USER (SYS_ID, USER_ID);

```