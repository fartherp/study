# spring事务传播性

---
##PROPAGATION_REQUIRED
###简介
```
加入当前已有事务；只有当前没有事务才启一个新的事务
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_REQUIRED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_REQUIRED
```
###案例
```
先调用ServiceA.methodA，发现没有运行在事务中，分配一个新事务。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），发现已经运行在ServiceA.methodA的事务内部，就不再启新的事务，而使用ServiceA.methodA事务。
```
###总结
```
在ServiceA.methodA或者在ServiceB.methodB内的任何地方出现异常，2个方法内部的操作，都会被事务回滚。
```

##PROPAGATION_SUPPORTS
###简介
```
如果当前在事务中，即以事务的形式运行，如果当前不在一个事务中，那么就以非事务的形式运行
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_REQUIRED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_SUPPORTS
```
###案例1
```
先调用ServiceA.methodA，发现没有运行在事务中，分配一个新事务。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），发现已经运行在ServiceA.methodA的事务内部，继续使用事务运行。
```
###案例2
```
直接调用ServiceB.methodB，发现没有运行在事务中，使用非事务运行。
```

##PROPAGATION_MANDATORY
###简介
```
支持当前事务，如果当前没有事务，就抛出异常
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_NOT_SUPPORTED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_MANDATORY
```

###案例
```
先调用ServiceA.methodA，发现没有运行在事务中，以非事务运行。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），发现已经运行在ServiceA.methodA的没有事务，抛出异常。
```

##PROPAGATION_REQUIRES_NEW
###简介
```
新建事务，如果当前存在事务，把当前事务挂起
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_REQUIRED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_REQUIRES_NEW
```
###案例
```
先调用ServiceA.methodA，发现没有运行在事务中，分配一个新事务。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），当执行到ServiceB.methodB的时候，ServiceA.methodA事务就会挂起，ServiceB.methodB启一个新的事务，等待ServiceB.methodB的事务完成以后，ServiceA.methodA的事务才继续执行。
```
###总结
```
ServiceB.methodB已经提交，那么ServiceA.methodA失败回滚，ServiceB.methodB是不会回滚的。如果ServiceB.methodB失败回滚，它抛出的异常被ServiceA.methodA捕获，ServiceA.methodA事务仍然可以提交。
```

##PROPAGATION_NOT_SUPPORTED
###简介
```
以非事务方式执行操作，如果当前存在事务，就把当前事务挂起
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_REQUIRED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_NOT_SUPPORTED
```
###案例
```
先调用ServiceA.methodA，发现没有运行在事务中，分配一个新事务。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），当执行到ServiceB.methodB的时候，ServiceA.methodA的事务挂起，ServiceB.methodB以非事务的状态运行完，再继续ServiceA.methodA的事务。
```
###总结
```
ServiceB.methodB数据操作出现异常不会回滚。
```

##PROPAGATION_NEVER
###简介
```
以非事务方式执行，如果当前存在事务，则抛出异常
```
###设计
```
类ServiceA,方法methodA,事务级别定义为PROPAGATION_REQUIRED
类ServiceB,方法methodB,事务级别定义为PROPAGATION_NEVER
```
###案例
```
先调用ServiceA.methodA，发现没有运行在事务中，分配一个新事务。再调用ServiceB.methodB（这个要写在ServiceA.methodA内部），抛出异常。
```

##PROPAGATION_NESTED
###简介
```
理解Nested的关键是savepoint
```
###总结
```
Nested的事务和它的父事务是相依的，它的提交是要等和它的父事务一块提交的。也就是说，如果父事务最后回滚，它也要回滚的。而Nested事务的好处是它有一个savepoint。也就是说ServiceB.methodB失败回滚，那么ServiceA.methodA也会回滚到savepoint点上，ServiceA.methodA可以选择另外一个分支，比如ServiceC.methodC，继续执行，来尝试完成自己的事务。但是这个事务并没有在EJB标准中定义
```



