#SpringMVC相关知识

### 1.拦截器的实现原理/方式：

1.继承HandlerInterceptor,重写PreHandle()，postHandle(),afterCompletion()三个方法；

2.在配置文件里面配置
<mvc:interceptors> <bean class="com.springmvc.config.SimpleHandlerInterceptor" /> </mvc:interceptors>


### 2.Spring MVC运行流程

1.客户端请求发送到DispatcherServlet

2.DispatcherServlet发送请求到HandleMapping

3.HandlerAdatper找到对应Handler

4.Handler执行对应Controller方法，返回ModelOrView

5.通过ViewResolver解析视图

6.渲染视图，将model包装在Response响应返回

7.返回客户端结果
