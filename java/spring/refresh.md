Spring容器创建之后，会调用它的refresh方法，refresh的时候会做很多事情：比如完成配置类的解析、各种BeanFactoryPostProcessor和BeanPostProcessor的注册、国际化配置的初始化、web内置容器的构造等等。





[refresh过程](https://fangjian0423.github.io/2017/05/10/springboot-context-refresh/)