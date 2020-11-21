## 生命周期
### 创建
分为 singleton 和 prototyoe

### 初始化
构造方法

注入

postProcessBeforeInitialization

initializingBean
或者自定义的方法 init-method

postProcessAfterInitialization

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