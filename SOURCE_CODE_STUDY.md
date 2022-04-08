# 执行器注册流程

```shell
1. init JobHandler Repository
2. refresh GlueFactory
3. super start
   init logpath
   init invoker, admin-client   利用反射，向注册中心注册自己，并将adminBiz缓存起来
   init JobLogFileCleanThread   处理jobLog日志
   init TriggerCallbackThread   处理 触发周期性 回调，  callback 和 retry
   init executor-server         initRpcProvider  启动serviceRegister注册  
   init, provider factory       （ExecutorServiceRegistry）      
   add services        将该执行器以服务的形式加入
   start               会利用netty 开启一个server, port: 9999,
   还会开启有一个ExecutorRegistryThread线程，不断地注册自己  
```
   
# 参考

3. xxl-job原理-- 执行器注册
[https://www.jianshu.com/p/d70b78a704e5](https://www.jianshu.com/p/d70b78a704e5)

6. xxl-job 原理-- 调度中心注册
[https://www.jianshu.com/p/8e148593627b](https://www.jianshu.com/p/8e148593627b)