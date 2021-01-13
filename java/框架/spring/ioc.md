## ioc的生命周期
读取 xml，获取配置信息
对配置信息做解析
利用反射构造对象，'完成 beandefination',IOC容器根据BeanDefinition进行实例化、配置以及组装Bean。
如果是 sington对象的话，直接创建



实例化：在堆中开辟一块新空间，属性都是默认值

初始化：给属性完成赋值



### application BeanFactory



the *ApplicationContext* is a sub-interface of the *BeanFactory*. Hence, it offers all the functionalities of *BeanFactory.*

Furthermore, it **provides** **more enterprise-specific functionalities**. The important features of *ApplicationContext* are **resolving messages, supporting internationalization, publishing events, and application-layer specific contexts**. This is why we use it as the default Spring container.



a. 国际化支持
b. 资源访问：Resource rs = ctx. getResource(“classpath:config.properties”), “file:c:/config.properties”
c. 事件传递：通过实现ApplicationContextAware接口

Bean的自动装配

refer

[spring application beanfactory](https://www.baeldung.com/spring-application-context)