

## 两大功能

依赖管理

开发导入starter场景启动器

无需关注版本号

可以修改版本号



自动配置

- 自动配好Tomcat

- - 引入Tomcat依赖。
  - 配置Tomcat

## 特点

1.  约定大于配置



## 原理


## 相关注解
1. springBootApplication
    这个注解对应的类，是springboot的主类 
    
1.  springbootconfiguration 配置类 == 配置文件，也是一个组件 @component
  
3. `@ComponentScan`扫描我们自定义的bean

4. enableconfiguration 开启自动配置 
      1. @autoconfigrationpackage,spring的底层注解@import(),给容器中导入组件

      2. 将主配置类所属的包，所在包的所有组件导入到容器中 类似于 <component-scan>

         





@import

导入相关的配置类





### @Configuration

- 基本使用
- **Full模式与Lite模式**

- - 示例
  - 最佳实战

- - - 配置 类组件之间无依赖关系用Lite模式加速容器启动过程，减少判断
    - 配置类组件之间有依赖关系，方法会被调用得到之前单实例组件，用Full模式







[springboot 原理](https://www.cnblogs.com/yewy/p/13194696.html)