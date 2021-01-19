## 自动配置原理

@ENableAutoConfigration

找到，meta-INF/spring.factories

对里面的类，进行加载



@Conditional

判断是否满足条件。有没有类，是不是在web应用这种





@ImportResource

引入xml 文件配置

```java
@ImportResource("classpath:beans.xml")
public class MyConfig {}
```

```xml
======================beans.xml=========================
<?xml version="1.0" encoding="UTF-8"?>
<beans>

    <bean id="haha" class="com.atguigu.boot.bean.User">
    </bean>
</beans>
```





[尚硅谷 spring boot](https://www.yuque.com/atguigu/springboot/qb7hy2#omZtW)

