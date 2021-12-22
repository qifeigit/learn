 Log4j-2中存在JNDI注入漏洞，当程序将用户输入的数据进行日志记录时，即可触发此漏洞，成功利用此漏洞可以在**目标服务器上执行任意代码。**

因该组件使用极为广泛，利用门槛很低，危害极大

风险等级：严重

# 影响范围：2.0-beta9 to 2.14.1（2021.12.10上午之前所有版本）

# 修复方案 

最新修复方案已更新

1. ##### 升级 Log4j2 至 **2.17.0** 及以上版本（建议修复方案）

下载地址：https://logging.apache.org/log4j/2.x/download.html

注：升级完成后请进行验证，并监控业务是否受影响。

# 组件自查方案

（Log4j2为基础组件，大部分项目均会引用）

#### **Maven 项目**

在本地项目或者服务器上执行以下命令：

```
mvn dependency:tree -Dincludes=org.apache.logging.log4j:log4j-core
```

如出现带有log4j关键字的内容结果，并且版本大于2.0，则表示项目存在此组件。如出现log4j内容，则表示项目存在此应用。

![img](../../../img/log4j2.2)

#### Gradle项目

在本地或者服务器上执行以下命令：

```
gradle :app:dependencyInsight --dependency org.apache.logging.log4j:log4j-core  --configuration releaseCompileClasspath -x test
```

如出现带有log4j关键字的内容结果，并且版本大于2.0，则表示项目存在此组件。如出现log4j内容，则表示项目存在此应用。

#### **其他类型项目**

请检查项目中是否调用了 log4j 2.0 以上版本的组件。

# 自我验证

修复完成以后，我们可以采用以下代码进行安全验证。

```
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import sun.applet.Main;

@RestController
public class HelloController {

    private static final Logger logger = LogManager.getLogger(Main.class);

    @RequestMapping(value = "hello")
    public String Hello(){
        String str = "Try ${date:YY-mm-dd}";
        logger.error(str);
        return "hello";
    }
}
```

如果输出内容为原样输出：

![img](../../../log4j2.3)

则表示修复成功。

如果输出内容为：

![img](../../../img/lo4j21)

则表示修复失败，请联系安全同事协助处理。