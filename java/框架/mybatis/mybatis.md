# mybatis

orm object relational mapping



创建  sqlsessionFactory  工厂

使用工厂生产 sqlsesesion

使用sqlsession 创建 Dao接口的代理对象



## 配置

环境



别名 

```xml
<typeAliases>
    <package name="org.sang.bean"/>
</typeAliases>
```

```java
@alias("user")
public class User{

}
```







