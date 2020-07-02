 ### Spring Bean的作用域：通过scope属性
 1.singleton:每次通过IOC容器返回的Bean实例都是同一个Bean实例
 2.prototype:每次通过IOC容器返回一个新的Bean实例，有状态的Bean使用
 3.reques:适用于http请求环境，每次请求返回一个新的Bean实例
 4.session:每一个session一个Bean实例
 5.global-session :所有session共享一个Bean实例


