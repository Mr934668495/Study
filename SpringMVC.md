#SpringMVC相关知识

###拦截器的实现原理/方式：
1.继承HandlerInterceptor,重写PreHandle()，postHandle(),afterCompletion()三个方法；

2.在配置文件里面配置
<mvc:interceptors> <bean class="com.springmvc.config.SimpleHandlerInterceptor" /> </mvc:interceptors>

即可
