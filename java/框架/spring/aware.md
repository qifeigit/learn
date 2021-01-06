### Spring提供一些Aware接口

看到Spring源码中接口以Aware结尾的接口(XXXAware)在Spring中表示对XXX可以感知,通俗点解释就是:如果在某个类里面想要使用spring的一些东西,就可以通过实现XXXAware接口告诉Spring,Spring看到后就会给你送过来,而接收的方式是通过实现接口唯一方法set-XXX.比如:有一个类想要使用当前的ApplicationContext,那么我们只需要让它实现ApplicationContextAware接口,然后实现接口中的唯一方法



**1 `beanNameAware`接口**：如果某个bean需要访问配置文件中本身bean的id属性，这个Bean类通过实现该接口，在依赖关系确定之后，初始化方法之前，提供回调自身的能力，从而获得本身bean的id属性，该接口提供了

```java
void setBeanName(String name);
```

方法实现，需要指出的是该方法的name参数就是该bean的id属性，加调该setBeanName方法可以让bean获取得自身的id属性