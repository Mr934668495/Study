# Spring的一些知识点：
### 1.Spring Bean的作用域：通过scope属性
 1.singleton:每次通过IOC容器返回的Bean实例都是同一个Bean实例

 2.prototype:每次通过IOC容器返回一个新的Bean实例，有状态的Bean使用

 3.reques:适用于http请求环境，每次请求返回一个新的Bean实例

 4.session:每一个session一个Bean实例

 5.global-session :所有session共享一个Bean实例

### 2.Spring Bean 的生命周期：
1.Bean实例的创建

2.为Bean实例设置属性

3.调用Bean的初始化方法

4.应用可以通过IOC容器使用Bean

5.当容器关闭时，调用Bean的销毁方法

### 3.Spring Bean 的加载过程：


### 4.Spring Bean 的注入：


### 5.BeanFactory 与ApplicationContext 是干什么的，两者的区别
BeanFactory是顶层容器，ApplicationContext是容器的高级实现；

### 6.BeanDefinition 的实现
BeanDefinition抽象了对Bean的定义，其是容器实现依赖反转功能的核心数据结构

### 7.Spring IOC容器的实现
Spring提供了各种各样的容器，有DefaultListableBeanFactory、FileSystemXmlApplicationContext等，这些容器都是基于BeanFactory，BeanFactory实现了容器的基础功能，包括containsBean能够判断容器是否含有指定名称的Bean，getBean获取指定名称参数的Bean等。

Spring通过refresh()方法对容器进行初始化和资源的载入

首先通过ResourceLoader的Resource接口定位到存储Bean信息的路径

第二个过程是BeanDefinition载入，把定义好的Bean表示成IOC容器的内部数据结构BeanDefinition，通过定义BeanDefinition来管理应用的各种对象及依赖关系，其是容器实现依赖反转功能的核心数据结构

第三个过程是BeanDefinition注册，容器解析得到BeanDefinition后，需要在容器中注册，这由IOC实现BeanDefinitionRegistry接口来实现，注册过程是IOC容器内部维护了一个ConcurrentHasmap来保存得到的BeanDefinition。如果某些Bean设置了lazyinit属性，Bean的依赖注入会在这个过程预先完成，而不需要等到第一次使用Bean的时候才触发。


### 8.Spring AOP
    切点表达式：
    ```<aop:config><aop:pointcut expression="this(com.bjsxt.aop.TestService)" id="mypoint"/></aop:config>```
        execution：
            语法格式： execution(返回类型.包名.类名.方法名(参数表))
            应用：最常用。也是相对最通用。根据方法执行的标准，定义切点 如 事务  日志
                
        target：
            语法格式：target(包名.接口名）
            应用：为某一个具体的接口实现提供的配置。如 登录的时候需要执行的附属逻辑是比较多的。在不同的业务流程中，附属逻辑也不同。如，电商中，可能在登录的时候需要去执行购物车合并
            
        this ：
            语法：this（包名.接口名）
            应用：针对某个具体的代理提供的配置。比target切点粒度细致。因为目标对象可以多实现。
            
        within：
            语法： within（包名.*） 代表在包中的任意接口或类型都作为切点
            应用：针对某一个包提供的切点，粒度比target粗糙。如：某包中的所有接口都需要执行某附属逻辑。如 电商平台中的下订单，下订单服务中可能需要特定的逻辑（时间戳校验，库存检查等），这些逻辑，是其他业务线中不需要提供切面的
            
        args：
            语法： args(类型，类型.....) 代表方法的参数表符合要求的时候，作为切点，参数表是有顺序的
            应用：主要应用在参数校验中。如：登录的时候必须传递两个字符串参数（登录名和密码）。可以使用args来限定。配合这execution实现。如：execution(.*.xxx.*.login(..)) args(String,String)。是使用频率最低的表达式
