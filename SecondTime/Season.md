#Season学习
###一、创建Maven项目  

<img src="img/SecondTime/Season/season_create.png" alt="create" align=center /> 
* groupId 组名，公司或组织名，如trs.com.cn。
* artifacted 应用名，当前Maven项目(SeasonTest)在组中的唯一id，如season-test。
* Enable Auto-Import 自动导入pom.xml中设置的依赖到maven本地仓库。

###二、配置pom.xml
```xml
    <groupId>trs.com.cn</groupId>
    <artifactId>SeasonTests</artifactId>
    <version>1.0-SNAPSHOT</version>

    <!--添加打包格式-->
    <packaging>war</packaging>

    <!--添加season的支持-->
    <parent>
        <artifactId>season-parent</artifactId>
        <groupId>trs.com.cn</groupId>
        <version>1.2</version>
    </parent>

    <!--添加season-core的依赖-->
    <dependencies>
        <dependency>
            <groupId>trs.com.cn</groupId>
            <artifactId>season-core</artifactId>
        </dependency>
    </dependencies>

    <build>
        <finalName>SeasonTests</finalName>
        <plugins>
            <!--添加打包插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <!--添加海尔maven仓库地址-->
    <repositories>
        <repository>
            <id>haier-maven-repository</id>
            <url>http://test.haier.com/nexus/content/groups/public/</url>
        </repository>
    </repositories>
```

###三、创建启动类App

```java
package com.trs.config;
import com.season.core.spring.SeasonApplication;
import com.season.core.spring.SeasonRunner;

/**
 * Created by sunmeng on 2016/10/10.
 */
public class App extends SeasonApplication {
    public static void main(String[] args){

        SeasonRunner.run(App.class);
    }
}
```

###四、创建测试类HelloController
```java
package com.trs.controller;
import com.season.core.Controller;
import com.season.core.ControllerKey;

/**
 * Created by sunmeng on 2016/10/10.
 */
@ControllerKey("hello")
public class HelloController extends Controller{

    public void season(){
        renderText("Hello Season!");
    }
}
```

###五、运行main()函数  

访问 http://localhost:8080/hello/season，浏览器显示  

<img src="img/SecondTime/Season/season_result.png" width = "280" height = "110" alt="create" align=center />

###六、错误处理  
1. main()函数只能执行一次，再次执行则报错，如图：  

<img src="img/SecondTime/Season/season_error1.jpg" alt="error1" align=center />

***原因：*** *没有意识到多次执行main()函数会开启多个端口，导致互相影响。*

2.Maven插件的clean-install命令无法使用，无法正常install打包项目，如图：  

<img src="img/SecondTime/Season/season_error2.jpg" alt="error2" align=center />  

***原因：*** *根据错误提示意识到可能是jdk原因，多次更换jdk版本后依然报错，最后替换IDEA自带jdk版本，解决了此问题。猜想根本原因是本地jdk，jre文件安装出现了问题。*  

项目地址：[https://github.com/sunm8705/SeasonTests](https://github.com/sunm8705/SeasonTests)

