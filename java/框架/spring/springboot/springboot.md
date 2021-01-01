## 特点
1.  约定大于配置



## 原理


## 相关注解
1. springBootApplication
    这个注解对应的类，是springboot的主类 
1.  springbootconfiguration 配置类 == 配置文件，也是一个组件 @component
   
2. enableconfiguration 开启自动配置 
      1. @autoconfigrationpackage,spring的底层注解@import(),给容器中导入组件
      2. 将主配置类所属的包，所在包的所有组件导入到容器中 类似于 <component-scan>





@import

导入相关的配置类