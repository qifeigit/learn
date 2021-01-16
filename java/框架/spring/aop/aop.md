# aop

[TOC]



1. 创建原始对象（目标对象）

```java
public interface UserService {
    void register(User user);
    boolean login(String name, String password);
}
public class UserServiceImpl implements UserService {
    @Override
    public void register(User user) {
        System.out.println("UserServiceImpl.register 业务运算 + DAO");
    }

    @Override
    public boolean login(String name, String password) {
        System.out.println("UserServiceImpl.login 业务运算 + DAO");
        return true;
    }
}

```

1. 额外功能 `MethodBeforeAdvice` 接口

```java
public class Before implements MethodBeforeAdvice {
    /**
     * 作用: 把需要运行在原始方法执行之前运行的额外功能, 书写在 before 方法中
     */
    @Override
    public void before(Method method, Object[] objects, Object o) throws Throwable {
        System.out.println("---method before advice log---");
    }
}
123456789
<!-- 额外功能 -->
<bean id="before" class="com.yusael.aop.Before"/>

```

1. 定义 **切入点**：额外功能的加入
   ⽬的: 由程序员根据⾃⼰的需要，决定额外功能加入给哪个原始方法(register、login)

```xml
 <!--切入点:额外功能的加入-->
    <!--⽬的: 由程序员根据⾃⼰的需要，决定额外功能加入给哪个原始方法(register、login)-->
   <!-- 简单的测试：所有方法都做为切入点，都加入额外的功能-->
    <aop:config>
        <aop:pointcut id="pc" expression="execution(* * (..))"/>
    </aop:config>
123456
```

组装（2、3 整合）

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/aop
                           https://www.springframework.org/schema/aop/spring-aop.xsd">
	
	<bean id="userService" class="com.yusael.aop.UserServiceImpl"/>
    <!-- 额外功能 -->
    <bean id="before" class="com.yusael.aop.Before"/>

    <!--切入点:额外功能的加入-->
    <!--⽬的：由程序员根据⾃⼰的需要，决定额外功能加入给哪个原始方法(register、login)-->
   <!-- 简单的测试：所有方法都做为切入点，都加入额外的功能-->
    <aop:config>
        <aop:pointcut id="pc" expression="execution(* * (..))"/>
        <!--表达的含义: 所有的方法 都加入before的额外功能-->
        <aop:advisor advice-ref="before" pointcut-ref="pc"/>
    </aop:config>

</beans>
```

1. 调用

   目的：获得 Spring 工厂创建的动态代理对象，并进行调用

   注意：

   1. Spring 的工厂通过原始对象的 id 值获得的是代理对象
   2. 获得代理对象后，可以通过声明接口类型，进行对象的存储

```java
/**
 * 用于测试动态代理
 */
@Test
public void test1() {
    ClassPathXmlApplicationContext ctx = new ClassPathXmlApplicationContext("/applicationContext.xml");
    UserService userService = (UserService) ctx.getBean("userService");
    userService.login("admin", "1234");
    userService.register(new User());
}

```





## 动态代理细节分析

Spring 创建的动态代理类在哪里？

- Spring 框架在运行时，通过动态字节码技术，在 JVM 创建的，运行在 JVM 内部，等程序结束后，会和 JVM 一起消失。



### 额外功能



##  methodInterception

可以运行在目标代码前，后，前后，异常

可以影响原始方法的返回值

## 切入点

```xml
<aop:pointcut id="pc" expression="execution(* * (..))"/>
```

对 execution（切入点函数） 做修改

第一 * ，代表返回符

第二 *，代表方法

第三(..)，代表参数



但这样匹配不精确，怎么更精准呢

引入 包，类，方法，参数



## 切入点函数

execution 功能最全面

args 参数的

within 包，类



## 切面

包括 切入点 和 额外功能



## 动态代理

如何创建动态代理类

jdk动态代理，第三方cglib



jdk动态代理需要原始类继承接口



cglib 继承了原始类





## 注解

