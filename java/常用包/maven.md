[Mac安装和配置Maven](https://www.cnblogs.com/lilyo/p/12887859.html)



## 路径依赖



http://www.itsoku.com/article/237#menu_22







### plugin



maven-dependency-plugin的功能：

1. 它会强制要求你在pom中直接声明程序中所用到的包，否则编译失败，这就避免了传递依赖；
2. 它会强制要求你的pom中不能声明任何多余的依赖，否则便以失败，这就避免了引入多余的无用的依赖



## maven-enforce-plugin


通过maven-enforcer-plugin可以强制要求项目遵守某些规范，例如JDK版本、Maven版本、某个插件版本、操作系统、某个文件的存在等。我们使用它限制某些某些包不能出现在依赖中。



### 路径分析



mvn dependency:tree

