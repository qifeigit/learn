## ioc的生命周期
读取 xml，获取配置信息
对配置信息做解析
利用反射构造对象，'完成 beandefination',IOC容器根据BeanDefinition进行实例化、配置以及组装Bean。
如果是 sington对象的话，直接创建



实例化：在堆中开辟一块新空间，属性都是默认值

初始化：给属性完成赋值

