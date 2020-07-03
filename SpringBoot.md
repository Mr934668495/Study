# SpringBoot

### 自定义starter参考：

https://mp.weixin.qq.com/s/F_1j-ng49QNlbj04Q9bqFQ

### SpringBoot启动流程：
1.启动类里面调用SpringApplication.run方法

2.在run方法中，首先构造SpringApplication对象，然后再调用run方法

3.在构造SpringApplication对象中，做了如下工作

。将sources放入primarySources变量中
。判断webApplication是什么类型的
。设置ApplicationContextInitializer，ApplicationListener，通过加载META-INF/spring.factories中配置的类
。找到main方法找到启动主类

4.run方法中，做的工作

。StopWatch主要是监控启动过程，统计启动时间，检测应用是否已经启动或者停止。

。加载SpringApplicationRunListener(也是通过META-INF/spring.factories),默认加载的是EventPublishingRunListener

。调用RunListener.starting()方法。

。根据args创建应用参数解析器ApplicationArguments;

。准备环境变量：获取环境变量environment，将应用参数放入到环境变量持有对象中，监听器监听环境变量对象的变化(listener.environmentPrepared)

。打印Banner信息(SpringBootBanner)

。创建SpringBoot的应用上下文(AnnotationConfigEmbeddedWebApplicationContext)

。prepareContext上下文之前的准备

。refreshContext刷新上下文

。afterRefresh(ApplicationRunner,CommandLineRunner接口实现类的启动)

。返回上下文对象
