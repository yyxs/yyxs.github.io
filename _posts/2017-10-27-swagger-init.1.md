---
layout: post
title:  spring mvc 集成swagger
subtitle: 'Tools'
date: 2017-10-27T00:00:00.000Z
author: yyxs
catalog: true
tags:
  - tools
---


## What is swagger?
Swagger is the world’s largest framework of API developer tools for the OpenAPI Specification(OAS), enabling development across the entire API lifecycle, from design and documentation, to test and deployment.

Swagger™的目标是为REST APIs 定义一个标准的，与语言无关的接口，使人和计算机在看不到源码或者看不到文档或者不能通过网络流量检测的情况下能发现和理解各种服务的功能。当服务通过Swagger定义，消费者就能与远程的服务互动通过少量的实现逻辑。类似于低级编程接口，Swagger去掉了调用服务时的很多猜测。浏览 Swagger-Spec 去了解更多关于Swagger 项目的信息，包括附加的支持其他语言的库。

## spring mvc 集成swagger

### maven pom 文件配置

采用的是springfox,pom文件依赖如下

```xml
    <!-- swagger2核心依赖 --> 
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-swagger2</artifactId>
        <version>2.7.0</version>
    </dependency>
    <!-- swagger-ui为项目提供api展示及测试的界面 --> 
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-swagger-ui</artifactId>
        <version>2.7.0</version>
    </dependency>
    <!-- 实现输出静态api文档 -->
    <dependency>
        <groupId>io.springfox</groupId>
        <artifactId>springfox-staticdocs</artifactId>
        <version>2.6.1</version>
    </dependency>
``` 
### Spring Java Configuration

```java
@Profile({"test"})
@Configuration
@EnableSwagger2
public class SwaggerConfig {

    @Bean
    public Docket userApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .groupName("APPV1")
                .select()  // 选择那些路径和api会生成document
                .apis(RequestHandlerSelectors.basePackage("com..."))
                .paths(PathSelectors.any()) // 对所有路径进行监控
                .build()
                .globalOperationParameters(setHeaderToken())
                .apiInfo(userInfo());
    }

    private ApiInfo userInfo() {
        Collection<VendorExtension> vendorExtensions = new ArrayList<>();
        ApiInfo apiInfo = new ApiInfo("相关接口",//大标题
                "相关接口，包括。。。",//小标题
                "1.0",//版本
                "杭州",
                new Contact("apple", "", ""),// 作者
                "swagger url",//链接显示文字
                "",//网站链接
                vendorExtensions
        );
        return apiInfo;
    }

}
```

### Spring xml Configuration

WebApplicationContext.xml 中添加上面的swagger配置类

```xml
  <mvc:annotation-driven/> 
  <bean class="com..............SwaggerConfig" />
```

## 启动web工程

以上配置完成后，即可启动项目，访问下面图片中的链接，搞定！！！

![avatar](/img/swagger-index.png)


