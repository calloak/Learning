# Spring Boot学习
###一、初步认识
####Spring Boot是什么？
1.spring boot只是对spring projects的一个封装，基于其他的Spring组件。  

2.该项目旨在帮助开发者更容易地创建基于Spring的应用程序和服务， 使得Spring开发者能够最快速地获得所需要的Spring功能。  

3.本身并不提供Spring框架的核心特性以及扩展功能，只是用于快速、敏捷地开发新一代基于Spring框架的应用程序。 也就是说，它并不是用来替代Spring的解决方案，而是和Spring框架紧密结合用于提升Spring开发者体验的工具。  

####优点是什么？
1.不用自己做配置，集中式配置，搭建速度快，降低学习门槛， 解决配置繁琐的问题，最大化的实现约定大于配置。 没有web.xml或者SpringMVC中dispatchServlet那样繁琐的配置。  

2.懂Maven会看文档就能开始一个新项目。

3.方便地让spring生态圈和其他工具链整合(比如Jackson, JDBC, Mongo, Redis,Mail)，来开发RESTFulService以及方便和数据库的交互。

4.提供了Spring各个插件的基于Maven的pom模板配置，开箱即用， 可以通过修改默认值来快速满足你的项目的需求，便利无比。

5.内置Tomcat和Jetty容器，可直接打成jar包启动，无需提供Java war包，无需将项目部署在tomcat。

6.提供了一系列大型项目中常见的非功能性特性，如安全、指标，健康检测、外部配置等。

7.SpringBoot对Maven及Gradle等构建工具支持力度非常大。其内置一个’Starter POM’，对项目构建进行了高度封装，最大化简化项目构建的配置。另外对Maven 和Gradle都有相应的插件，打包、运行无需编写额外的脚本。  

####缺点是什么？
1.因为不用自己做配置，有时，启动时不知道框架哪里抽风， 会导致系统无法启动，报的错都很神奇，难以找到解决方案。

2.入门容易，但是如果没有完整学习spring的体系，碰到问题就报国无门。

###二、搭建Spring Boot的Demo
1.创建 Maven 项目  

2.在pom.xml中引入Spring Boot的依赖 

```xml
    <groupId>trs.com.cn</groupId>
    <artifactId>springboot-test</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.2.5.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```
3.编写一个测试类BootTest及main()函数  

<img src="img/SecondTime/SpringBoot/spring_BootTest.png" width = "200" height = "230" alt="BootTest测试类" align=center />

```java
package com.trs.test;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.stereotype.Controller;

/**
 * Created by sunmeng on 2016/10/10.
 */
@Controller
@EnableAutoConfiguration
public class BootTest {

    @RequestMapping("/")
    @ResponseBody
    String home() {
    
        return "Hello World!";
    }

    public static void main(String[] args) {

        SpringApplication.run(BootTest.class, args);
    }
}
```
* @Controller 用于标注控制层组件。  
* @EnableAutoConfiguration 开启Spring事务管理，相当于XMl中的<tx:*>；使用Spring MVC框架的一些默认配置；会初始化一个Scheduler用于执行定时任务和异步任务
* @RequestMapping 是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。
* @Responsebody 表示该方法的返回结果直接写入HTTP response body中，一般在异步获取数据时使用，在使用@RequestMapping后，返回值通常解析为跳转路径，加上@Responsebody后返回结果不会被解析为跳转路径，而是直接写入HTTP response body中。比如异步获取json数据，加上@Responsebody后，会直接返回json数据。  

4.启动main()函数  

在Tomcat启动后，访问http://localhost:8080就可以看到Hello BootTest!出现在浏览器中了。  

<img src="img/SecondTime/SpringBoot/spring_print.png" width = "260" height = "180" alt="显示" align=center />  

项目地址：[https://github.com/sunm8705/SpringBootTest](https://github.com/sunm8705/SpringBootTest)
