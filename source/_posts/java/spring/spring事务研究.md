---
title: spring事务研究
categories: 
- [java, spring]
tags: 
- 事务
- 持续更新
---
# @transactional
@transactional 采用aop代理生成事务,如果调用的方法不是spring生成的代理类，注解不生效，比如同类方法间的调用
```java
@transactional
public void a() {
...
}

public void b() {
  this.a()
}
```