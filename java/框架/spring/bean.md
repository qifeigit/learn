## 生命周期
### 创建
分为 singleton 和 prototype

singleton会在工厂初始化的时候就被创建

prototype则会在获取bean对象的时候创建



元信息配置解析阶段

bean 注册阶段

bean实例化阶段：调用构造方法创建对象

依赖注入

bean属性赋值阶段

检查 aware相关接口

postProcessBeforeInitialization

@postConstruct

initializingBean

自定义的方法 init-method

postProcessAfterInitialization



使用bean



@preDestroy

disposableBean



1.顺序 

2.注入⼀定发⽣在初始化操作的前面。

3.什么叫做初始化操作

​	对资源的初始化 数据库 io 网络



BeanPostProcessor
初始化后完成





### 销毁

- 什么时候销毁对象

  ​	工厂关闭的时候

disposeBean
xml 中的 destroy-method

对资源的释放





