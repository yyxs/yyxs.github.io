---
layout: post
title:  cucumber background 与 hooks
subtitle: '自动化测试'
date: 2017-10-30T00:00:00.000Z
author: yyxs
catalog: true
tags:
  - 自动化测试
---

## Background

Background allows you to add some context to the scenarios in a single feature.  
[Background允许你可以在某些特定的scenarios中添加一些上下文]  
A Background is much like a scenario containing a number of steps.[Background更像是包含多个步骤的scenarios]  
The difference is when it is run.The background is run before each of your scenarios but after any of your Before Hooks.  
[不同的是当运行时，Background运行在你的scenarios之前但是在Hooks之后]  

### Background举例

```feature
  Feature: 登录到管理后台
  
  Background:
    Given 打开登录页面
    When 输入用户名: "admin"
    When 输入密码: "123456"
    Then 点击【登录】按钮

  Scenario: 正常登录
    Given 打开车辆待审核页面
```

## Hooks

Cucumber provides a number of hooks which allow us to run blocks at various points in the Cucumber test cycle.  
[Cucumber提供了一些hooks这些允许我们在Cucumber的运行期各种节点上运行blocks]  
You can put them in your support/env.rb file or any other file under the support directory, for example in a file called  support/hooks.rb.
[你可以将hooks文件放在任何支持的目录下，比如说support/hooks.rb]  
There is no association between where the hook is defined and which scenario/step it is run for  
[hook文件定义和场景|步骤并没有联系]  
All defined hooks are run whenever the relevant event occurs.  

### Hooks举例
```java
import cucumber.api.java.After;
import cucumber.api.java.Before;
public class HooksDemo {

    @Before
    public void beforeScenario(){
        System.out.println("This will run before the Scenario");
    }

    @After
    public void afterScenario(){
        System.out.println("This will run after the Scenario");
    }
}
```

## 总结
以上Background和Hooks都是为了自动化测试时能分离出一些抽象模块，供复用，DRY原则。

